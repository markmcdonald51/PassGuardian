# PassGuardian

Never store your secrets in one place again.

Store and share your secrets safely by splitting them into cryptographically-secure pieces. To reconstruct the original, combine a specific number of these pieces. It's simple, secure, and free.



Configurable levels of confidentiality and reliability
Secret sharing is a method for distributing a secret among participants or locations. A secret can consist of any data; for example, a password, a message, an account number, an ecnryption key, missile launch codes, or a Bitcoin private key all represent highly sensitive and important secrets. Traditionally, when guarding highly sensitive information, one would have to choose between keeping a single copy of the secret in one location for maximum secrecy, or keeping multiple copies of the secret in different locations for greater reliability. By increasing storage locations or entrusted parties, reliability is increased at the expense of secrecy. Secret sharing addresses this problem by allowing arbitrarily high levels of confidentiality and reliability.

The process of splitting a secret results in a specified number of shares of the secret. Each share is a random number that by itself provides no information about the secret. The secret can be reconstructed only when a sufficient number (threshold) of shares are combined. During the splitting process, one can select the number of shares to create and the threshold needed to reconstruct the secret.

Note that during the reconstruction process, a reconstruction is computed for any number of shares. If the number of shares is less than the threshold, this reconstruction of the secret will be INCORRECT.

During the share-creation process in advanced mode, PassGuardian also computes a SHA3-512 cryptographic hash of the secret. This is a unique hash that can be used to verify the authenticity of any reconstructed secret, as the hash of the reconstruction should match the hash of the secret. The secret cannot be derived from the hash. Distribution of this hash is optional, and should only be used to aid in verifying data integrity.

A proven cryptographic algorithm
The secret sharing method that PassGuardian employs is based on Shamir's threshold secret sharing scheme, named after its discoverer Adi Shamir. His 1979 landmark paper, "How to Share a Secret" [PDF, 70kb], provides the background for this threshold sharing scheme. One of the most useful properties of Shamir's sharing scheme is that it is "information-theoretically secure" and "perfectly secure", in that less than the requisite number of shares provide no information about the secret (i.e. knowing less than the requisite number of shares is the same as knowing none of the shares).

Open-source, verifiable implementation
PassGuardian is built on secrets.js, an open-source implementation of Shamir's sharing scheme. While secrets.js permits Galois Fields up to 20 bits in size, PassGuardian uses an 8-bit binary finite field for computations. The share format is described at the secrets.js page.

Privacy and security
All computations are done in your browser. No secrets or secret shares are ever transmitted back to our servers. Once the PassGuardian page is loaded in your browser, it can be run offline. For maximum security, it is recommended that you perform computations offline.

Like most website operators, PassGuardian collects non-personally-identifying analytics information of the sort that web browsers and servers typically make available, such as the browser type, language preference, referring site, and the date and time of each visitor request. PassGuardian's purpose in collecting non-personally identifying information is to better understand how visitors use its website.

PassGuardian requires the availability of a cryptographically-strong pseudo-random number generator (CSPRNG) during the secret splitting phase only. If a strong PRNG is not found during run-time, PassGuardian will use the built-in Math.random(), which is NOT cryptographically secure. Consider upgrading to a newer browser that supports crypto.getRandomValues() to take advantage of the increased security that this PRNG provides.



Use cases
There are many scenarios where secret sharing is useful. Some interesting examples are:
Reliable distributed classified data storage
Shares can be stored on multiple servers and in multiple locations. A security breach in one or more locations would be insufficient to recover the sensitive data. A server breakdown in one or more locations would not necessarily mean loss of classified data, as long as a threshold number of shares remain accessible.

Sharing sensitive information via insecure channels
Shares can be distributed via a combination of secure and insecure channels and media and combined by the recipient to reconstruct the original data. Interception of less than the threshold number of shares would be insufficient to reconstruct the original secret.

Voting and hierarchical delegation of authority
Shares can be distributed to members of a committee. For a policy or process to be initiated, a majority of the members must be present with their shares. A variation of this scenario is when different members are assigned different voting powers by holding different quantities of shares. For example, a bank manager might hold 5 shares of a vault key, and each of his or her subordinate supervisors might hold 1 share. The bank manager's 5 shares are sufficient to unlock the vault, but all 5 supervisors must be present to perform the same task. This can be extended to arbitrary hierarchical schemes where each share is re-shared with a different number of participants, delegating various levels of responsibility and power to the participants.

An interesting example of this is the division of the DNSSEC root key among 7 Trusted Community Representatives (TCR). DNSSEC is the backbone of internet security and the "root zone" is signed with a key. While the DNSSEC Practice Statement doesn't state what sharing scheme is employed, it is feasible that Shamir's secret sharing is used in a (7,5) configuration, i.e. 5 of the 7 TCRs must be present to reconstruct the root key.

Executing wills
Distribute shares of your passwords, account numbers, etc to trusted parties or family members. All of the parties must be present to gain access to your accounts and private data.



Powered by secrets.js
Written by 2015 Alexander Stetsyuk <alex AT passguardian.com>
