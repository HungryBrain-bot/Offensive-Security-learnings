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

** Before going into detailed explaination of NTLM protocol we will look into, type of NTLM hashs, Important NTLM attacks [Click here](#NTLM in detail) ** 

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




