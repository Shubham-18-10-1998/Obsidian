# Authentication
- Validating user identity
- Types
	- Two factor authentication
	- Username, email, password
- Ideally every call is authenticated. To prevent constant login for every call we have 
	- Two types
		- Token based
		- Session based
- Flow
	- Register -> Verify Registration -> Login -> Session Based Authentication
- ![[Pasted image 20260108205049.png]]
- Browser stores essentially a credential to validate all calls. 
	- Can be session id
	- Can be token
	- Responsibility of front-end to store this in browser cache
- ## Token Based  
	- Stateless - Is self descriptive. Server doesn't store anything
	- Gets expired after some time. 
		- Refresh Token
	- Server only generates, and then it has everything. Through encoding, encryption and hashing
	- Like a movie ticket, The ticket has all information so the theatre dioesnt need to store any information, it only needs to validate it.
	- [[Working of signing in JWT tokens Explanation]]
	- Key Anaolgy
		- Private key is like the hologram with invisible ink that only you can generate
		- Public key is like the UV reader that everyone has which they can use to verify the hologram.
	- ![[Pasted image 20260108210627.png]]
	- ### Keys
	- Keys used in token have two uses :
		- Encryption/Decryption (for secrecy)
		- Signing/Verification (for trust)
		- JWT uses signing, not encryption-decryption
		- Symmetric Key :
			- Shared locker key : Same key to lock-unlock
				- Token is signed with data secret
				- TRRo verify u need to know the same secret
		- Assymetric Key
			- Wax seal on letter
			- You write a letter and seal it with private seal(private key). Now anyone who knows the seal can verify to see its orignal or not(public seal design). But no one else should be able to create the private seal of the king
- ## Session Based
	- Stateful - Server stores the details. And it can also get you out of the session.
	- Server stores details for each session id.
	- Not encoded in nature
	- here its like giving you a id card with a id number which they store in security. very time they use the id number to get your information and then validate the user.
	- ![[Pasted image 20260108210204.png]]
	- Sticky Sessions enabled : Every request. has to hit the same server
		- hence they are harder to scale.
		- HOT - mServres : when uneven distribution.

## Encryption
- Encoding Decoding with respect to a secret

## Encoding
- Converting one representation to another which can be reversed.
	- Eg. Decimal to Binary
- Reverting to the original is called decoding
- No secret key involved
- Fully reversible
- Not for security

## Hashing
- Irreversible process of converting to gibberish
- Password matching, cause we don't want original information back. So that data is secure in case of hacking
- Two values should produce never produce same hash
	- This is conflicting
- MD5 -> Hash-Function
	- To prevent collisions -> 
	- Salting 
		- Adding some random value at the end so that their hash never collide.
	- Peppring
		- Adding same value everywhere thats a secret and not stored in the DB for security
- Secret key 
	- helps prevent different servers from accessing each others info.
- Key feaures
	- Deterministic : same input -> same result
	- Avalance : small change -> big difference in output
	- Fixed Size
	- One-way -> can't recover data here

### Comparison
|Technique|Secret?|Reversible?|Security?|
|---|---|---|---|
|Encoding|❌ No|✅ Yes|❌ No|
|Hashing|❌ No|❌ No|❌ No|
|Encryption|✅ Yes|✅ Yes|✅ Yes|
|Signing|✅ Yes|❌ (conceptually)|✅ Yes|

## Signing 
Only private key so that only that server can access. and another cant access it.

Working of Signing
Great — this is the **right final question** because now we’ll put **everything together into one end-to-end flow** and clearly separate:

- **What happens on the user side**
    
- **What happens on the server side**
    
- **Where signing and verification actually occur**
    
- **What keys live where**
    

I’ll explain this **step-by-step**, then give you a **mental model you can replay in your head**.

---

# 🧠 First: One critical clarification

❗ **The user NEVER signs anything with cryptographic keys.**

This is a very common misunderstanding.

👉 **Only the server signs**  
👉 **User just proves identity once (username/password)**  
👉 **Token signing happens on the server**

Now let’s walk the full flow.

---

# 🏗️ Actors Involved

We’ll assume **JWT with asymmetric signing (RS256)**.

### Actors

- 👤 User (browser / mobile app)
    
- 🔐 Auth Server
    
- 🧩 Resource Server (API)
    

### Keys

- 🔑 **Private key** → Auth server only
    
- 🔓 **Public key** → All servers that verify tokens
    

---

# 1️⃣ USER SIDE — Login (NO signing here)

### Step 1: User enters credentials

```
username = "shubham"
password = "hello123"
```

### Step 2: User sends login request

```
POST /login
{
  username,
  password
}
```

📌 At this point:

- No JWT
    
- No signing
    
- No keys involved
    

---

# 2️⃣ SERVER SIDE — Authentication (Still no signing)

### Step 3: Server verifies credentials

Server does:

```
hash(input_password + salt)
→ compare with stored hash
```

If match:  
✔ User is authenticated

---

# 3️⃣ SERVER SIDE — Signing happens HERE ✅

This is the **only place signing occurs**.

### Step 4: Server creates token payload

```json
{
  "sub": "shubham",
  "role": "USER",
  "exp": 1700000000
}
```

---

### Step 5: Server SIGNS the token

Internally:

```
hash(header + payload)
→ sign hash with PRIVATE KEY
→ signature
```

JWT created:

```
HEADER.PAYLOAD.SIGNATURE
```

🔐 **Private key never leaves server**

---

### Step 6: Server sends token to user

```
HTTP 200 OK
Authorization: Bearer <JWT>
```

---

# 🧠 Important Realization

👉 **User does NOT understand the token**  
👉 **User does NOT verify the token**  
👉 **User does NOT sign anything**

User just **stores and forwards** the token.

---

# 4️⃣ USER SIDE — Using the Token (Still no signing)

### Step 7: User calls API

```
GET /orders
Authorization: Bearer <JWT>
```

User is just acting like a **courier**.

---

# 5️⃣ SERVER SIDE — Verification happens HERE ✅

Every protected request:

### Step 8: Server extracts JWT

```
HEADER.PAYLOAD.SIGNATURE
```

---

### Step 9: Server verifies signature

Using **public key**:

```
hash(header + payload)
→ verify signature using PUBLIC KEY
```

✔ If valid:

- Token not tampered
    
- Token issued by trusted auth server
    

❌ If invalid:

- Reject request
    

---

### Step 10: Server checks claims

```
exp → not expired?
role → allowed?
```

---

### Step 11: Server authorizes request

```
return 200 OK
```

---

# 🔄 Full Flow in One Compact Diagram (Mental)

```
USER
 └── login (username/password)
        ↓
AUTH SERVER
 ├── verify password
 ├── create JWT
 ├── SIGN with private key
        ↓
USER
 └── sends JWT with every request
        ↓
RESOURCE SERVER
 ├── VERIFY signature with public key
 ├── read claims
 └── allow / deny
```

---

# 🔑 Where Keys Live (Very Important)

|Key|Location|
|---|---|
|Private key|Auth server only|
|Public key|All backend services|
|User|❌ No keys|

---

# 🔍 Why This Is Secure

### If attacker steals token:

- They can use it until expiry
    
- They **cannot modify it**
    
- They **cannot create new tokens**
    

### If attacker steals public key:

- No problem
    
- Public key cannot sign
    

### If attacker steals private key:

🚨 **System compromised**

---

# 🧠 Final Mental Model (Lock This In)

### User

> “I prove who I am once, then carry proof.”

### Auth Server

> “I issue signed proof.”

### API Server

> “I verify proof every time.”

---

# ✅ Answering Your Question Directly

> **How does it work on user side with signing in effect?**

✔ User never signs  
✔ User only sends credentials and later forwards token

> **How does it work on server side for verification?**

✔ Server verifies signature using public key  
✔ Server trusts payload only after verification

---

If you want next, I can:

- Show **Spring Security filter chain**
    
- Explain **access token vs refresh token**
    
- Explain **token expiration and rotation**
    
- Show **why logout is hard with JWT**
    

You now understand **real-world authentication architecture**, not just theory 👏

-----------------------


## Verification Token Flow
UserService method get User is over ride to authenticate

User ID is in VerficationToken ID
Token has User Entity as member where Relationship is one-one

This should be transactional as both processes are tightly coupled

Relationships are defined by the parent hence composition as user has token

OTP is harder to to implement, and mail better

WIth login with Token we have to return the token.


## Middleware 
Filters in springboot. Request comes here before going to the controllers


# Authorisation
- Giving the user necessary accesses/ privileges.
- Can only happen after authentication
- Role Backed 
- Global State for request context
- Clains inside the JWT token taken, then we set context, and then that is available to use everywhere.
- @PreAuhtorize("hasAnyRole(USER)")
- @EnableMethodSecurity
- For Session only two anotations above needed


Dependcies
- Spring Web
- Spring Security
- Data Jpa
- MySql Driver

We then get default session based authentication

Different between prseJWS and then parseJWT








Questions :

What is strength?
What is encoding, hasing, decoding
Token and Session
JWT and Session
Salting
Strength

