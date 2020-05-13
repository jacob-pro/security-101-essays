COMS10005_2018
Jacob Daniel Halsey (vw18148)

# Coursework 1

## Selected Article

Graham-McLay, Charlotte. "Fork Over Passwords or Pay the Price, New Zealand Tells Travelers." The New York Times. October 02, 2018. Accessed November 07, 2018. https://www.nytimes.com/2018/10/02/world/asia/new-zealand-passwords-devices.html.

## Securing data in transit: Plausible Deniability

The selected article is of particular interest to myself because my family and I are intending go on holiday to New Zealand next year. 

What risk does this pose? I currently use a Windows 10 laptop that has BitLocker enabled and is joined to my personal Active Directory domain. Surrendering my login credentials would therefore create a significant risk because it would not only grant the officers access to the laptop itself, but also to any of my other computers, including my email, file, and Remote Desktop servers, all accessible on the Internet. Furthermore it contains a password database file for many Internet services that I use, which they could also demand access too.

Fortunately the law is limited to an 'initial search' with 'any transmitting functions' disabled, and only allows for a 'full search' using 'cloning or other forensic methods' if there is reasonable cause to believe it contains evidence of criminal activity. However this relies on trusting the customs officers to actually follow the law; once I have allowed them to decrypt the drive, they could in practice quickly clone and do whatever they want with the data.

One potential solution is to replace BitLocker with VeraCrypt, which has a hidden operating system feature. First a partition is created to contain a decoy operating system. Then a second encrypted partition is created, ideally containing some fake sensitive information so as to justify its existence (the outer volume). However within this outer volume is a hidden volume containing the actual operating system and data. Depending on which password is supplied at startup will determine which operating system is booted.

The purpose of the hidden volume is to create plausible deniability: the contents of an encrypted volume compared to unused space (which would just be random data) should be indistinguishable. While the customs officers may demand access to the outer volume, they should not be able to prove the existence of the hidden volume, and therefore cannot demand access to it.

Unfortunately it is possible that VeraCrypt's implementation is flawed - Kedziora, Chow and Susilo claim that VeraCrypt leaves two areas 512 bytes long within the hidden OS partition that are 'not overwritten by the VeraCrypt encryption algorithm'. One contained a path to 'winload.exe' thereby indicating the existence of a hidden OS. However the lead developer idrassi has not been able to replicate these findings, and states that they are 'simply not true'. 

## References

"Customs and Excise Act 2018." Customs and Excise Act 2018 No 4 (as at 01 October 2018), Public Act – New Zealand Legislation. Accessed November 07, 2018. http://www.legislation.govt.nz/act/public/2018/0004/latest/whole.html.

"Hidden Operating System." VeraCrypt - Free Open Source Disk Encryption with Strong Security for the Paranoid. Accessed November 07, 2018. https://www.veracrypt.fr/en/VeraCrypt%20Hidden%20Operating%20System.html.

"Hidden Volume." VeraCrypt - Free Open Source Disk Encryption with Strong Security for the Paranoid. Accessed November 07, 2018. https://www.veracrypt.fr/en/Hidden%20Volume.html.

Kedziora, Michal, Yang-Wai Chow, and Willy Susilo. "Defeating Plausible Deniability of VeraCrypt Hidden Operating Systems." (2017).
http://ro.uow.edu.au/cgi/viewcontent.cgi?article=1542&context=eispapers1

"VeraCrypt." / Forums / General Discussion:Is Hidden OS Plausible Deniability Defeatable? Accessed November 07, 2018. https://sourceforge.net/p/veracrypt/discussion/general/thread/c3eab72a/.