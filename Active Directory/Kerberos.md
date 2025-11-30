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
       
