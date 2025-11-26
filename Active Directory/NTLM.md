NTLM (New Technology LAN Manager)
## Simple understanding of NTLM

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

** Before going into detailed explaination of NTLM protocol we will look into, type of NTLM hashs, Important NTLM attacks [Go to NTLM in detail](#NTLM in detail) ** 

NTLM Hash Types:
Hash Type         Example                     Purpose
--------------------------------------------------------------
LM Hash           Very weak, almost obsolete  Legacy systems
NT Hash           Main NTLM password hash     Used today
NTLMv2 Response   Stronger challenge response Most common

** The NTLM hash = MD4 hash of the password, not salted -> vulnerable **

Important NTLM Attacks:
Attack            Why possible
-------------------------------------------------------------
Pass-the-Hash     Login using NTLM hash instead of password
NTLM Relay        Forword authentication request to another target
Brute-force       Hashes unsalted -> fash cracking
SMB Capture       Capture challenge/response via responder via responder/mitm6

** Will explain these attacks in detail in future **


## NTLM in detail
How NTLMv2 authenticates ?
1. Client sends Negotiate message which allows the client to specify its supported NTLM options to the server. [Negotiate message](https://learn.microsoft.com/en-us/openspecs/windows_protocols/ms-nlmp/b34032e5-3aae-4bc6-84c3-c6d80eadf7f2)
2. Server after receiving the Negotiate message sends back the server challenge. It is used by the server to challenge the client to prove its identity. [Challenge message](https://learn.microsoft.com/en-us/openspecs/windows_protocols/ms-nlmp/801a4681-8809-4be9-ab0d-61dcfe762786)
3. In response to the server’s challenge message, the client creates an NTLMv2 hash by hashing the user’s password using MD4, then combining it with the username and domain. This intermediate hash is then combined with the server challenge and the client challenge to produce the NTLMv2 hash (response), which is sent to the server. [Response](https://learn.microsoft.com/en-us/openspecs/windows_protocols/ms-nlmp/033d32cc-88f9-4483-9bf2-b273055038ce)




