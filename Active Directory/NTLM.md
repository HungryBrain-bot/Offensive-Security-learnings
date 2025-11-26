NTLM (New Technology LAN Manager)
Simple understanding of NTLM
What is NTLM ?
- A challenge-response authentication protocol used by Windows systems primarily for:
  * Local authentication
  * Legacy systems
  * When Kerberos is not available
How NTLM Authenticates ?
1. Client sends username to server.
2. Server generates a challenge (random value) and sends it to client.
3. Client encrypts the challenge using the NTLM hash of the password and returnm the result.
4. Server verifies using the stored NTLM hash.

