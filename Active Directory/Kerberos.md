##Kerberos

Why Kerberos ?
* Kerberos is a robust and secure authentication protocol used in most modern environments.
* Kerberos ensures secure authentication using symmetric cryptography.
* It employs a ticket-based mechanism were the tickets are issued by the Key Distribution Center(KDC).

Kerberos: Ticket-granting Authentication (Authentication flow)
1. AS-REQ (Authentication Service Request)
   * The client sends a request to the KDC Authentication Service (AS)
   * The request contains the username and timestamp, encrypted with the user's password hash.
2. AS_REP (Authentication Service Reply)
   * The KDC checks the username in the database.
   * If the timestamp can be decrypted using the stored password hash -> user is verified.
   * The KDC then sends back:
     a) TCT (Ticket Granting Ticket)
     b) Session key
   The TGT allows the client to request access to services without re-entering the password.
3. TGS-REQ (Ticket Granting Service Request)
   * When the client to access a service (e.g., SMB, MSSQL) it sends:
     a) TGT
     b) Service name (SPN)
     c) Encrypted timestamp using the session key
     This request goes to the KDC Ticket Granting Service (TGS)
  4. TGS-REP (Ticket Granting Service Reply)
     * The KDC verifies the TGT.
     * If vaild, it issues a Service Ticket (aka ST), encrypted using the service account's password hash.
  5. AP-REQ (Application Request)
     * The client sends the Service Ticket to the target server hosting the service.
  6. AP-REP (Application Reply)
     * The server decrypt the service ticket using its own password hash.
     * If successful, mutual authentication is established and access is granted.

Why Kerberos attacks are possible ?
Kerberos is secure by design, but real-world Active Directory environments introduce weaknesses that attackers can exploit. Kerberos trusts information stored inside AD - and if AD has misconfigurations, weak passowrds, or over-privileged accounts, attacks become possible.

Main reasons Kerberos attack work ? 
* Kerberos depends on passowrd hashes - If an attacker can access a hash (e.g., service account), they can generate / forge tickets without the password
* Service account often have weak passwords - Makes SPN brute forcing (Kerberosting / AS-REPRoast) possible.
* Long-lived Kerberos tickets - Gives time for offline cracking and persistence.
* Misconfigured delegation - Allows attackers to impersonate other users/services
* High-privileged account tied to services - If SPN runs as Domain Admin -> compromising service ticket = Domain Admin
* KDC completely trusts the TGT - If attackers forge TGT (Golden Ticket), they bypass authentication entirely.
* No password attempt throttling - Offline cracking of hashes has no lockout risk

Major Kerberos attack techniques and the reason why they work.
* Kerberoasting - Service account password = used to encrypt service ticket -> weak password allows offline cracking
* AS-REPRoasting - Accounts without pre-authentication -> attackers can request AS-REP ciphertext and crack offline
* Pass-the-Ticket - Kerberos tickets are reusable -> if attackers steals a ticket, they can reuse it without the password
* Golden Ticket - If attacker gets KRBTGT hash, they can forge valid TGT's forver
* Silver Ticket - If attacker gets service account hash, they can forge service tickets fot that one service.
* Unconstrained delegation abuse - Allows hosts to store user TGT's -> attacker can steal them
* Constrained delegation abuse - Delegation settings allow attackers to impersonate users to specific services
* S4U / Resource-based delegation abuse - AD trusts SPN configuration -> attacker can modify delegation rights to impersonate users
       
