## Computer Security

_I am not a computer security expert but there's some basic computer security essentials that a surprising number of people don't understand. The aim of this doco is to raise awareness of this information._

## Passwords

Let's start with the basics of passwords with a quiz.

Which passport do you think is more secure? What do your passwords look more like?

a) `Tr0ub4dor&3`\
b) `correct-horse-battery-staple`

If you take a look at [howsecureismypassword.net](https://howsecureismypassword.net/) and put in these two passwords:

a) It would take a computer about 4 HUNDRED YEARS to crack your password\
b) It would take a computer about 1 OCTILLION YEARS to crack your password

This is because b) has a higher level of entropy, even though it is far easier to remember!

This [cartoon](https://xkcd.com/936/) explains this really well (and shows where I got the passwords!) and explains how we've trained everyone to use the wrong passwords!

[![password_strength](/media/password_strength.png)

There's a few things to remember about passwords:

1.  Never give your passwords to anyone else -- no matter how nicely they ask
2.  No two passwords should ever be the same -- even if they are "throw away" passwords
3.  You should use use pass-phrases like the example b) above for passwords you need to remember, all other passwords should be randomly generated to be at least 24 characters and have numbers, mixed case letters, and symbols -- and be stored in a password manager -- I'll cover password managers in my next post.
4.  Passwords and passphrases should not be constructed from known phrases. `Ph'nglui mglw'nafh Cthulhu R'lyeh wgah'nagl fhtagn1.` is a bad password; it was [cracked in minutes](https://arstechnica.com/security/2013/08/thereisnofatebutwhatwemake-turbo-charged-cracking-comes-to-long-passwords/) as it contains a known phrase from a short story called T*he Call of Cthulhu.*
5.  Don't store passwords in a Google Doc or other online document service even if it has two factor authentication -- use a password manager (which I will cover next post)

## Password Managers

As mentioned above, it's important to use a different password for every service you use and to have long and cryptic randomly generated passwords.

Our human brains can't remember the sheer quantity and complexity of passwords you'll need for day-to-day use so this is where password managers come in handy. A password manager is software that serves two main purposes: to generate long and complex passwords for you, and to store them so you don't need to remember them. You password manager database needs to be encrypted and you should use a passphrase based password that you can remember but is very long so it's hard to guess. I talked yesterday about high entropy passphrase based passwords.

The two most popular password managers are **[LastPass](https://www.lastpass.com/)** and **[1Password](https://1password.com/)** -- their names both imply that your password manager 'master' password is the only or last password you'll ever need to remember.

I've used both of these password managers; I found LastPass to be more affordable and 1Password to have a more polished user experience but YMMV. The thing I like about 1Password is their family plan which makes it easy to share vaults across family members and administer family members accounts. This is why I currently use 1Password.

Both of these password managers integrate well with browsers and mobile operating systems to able you to quickly pre-fill password information when required. 1Password on iOS has a Safari extension which populates logon forms so you don't need to use a special app or browser.

Both services have a cloud option to store your data which makes accessing it on your devices easy, but using a cloud service is less secure than just storing this data locally and syncing it to devices over local wifi which 1Password allows. 1Password has an account key which is used to access your data on new devices whereas LastPass optionally allows multi-factor authentication to access your passwords which you should use. I will cover multi-factor authentication in my next post.

If you don't currently use a password manager I would recommend you start using one of the two I mentioned straight away and begin storing all your passwords in it. You can use the 'generate secure password' feature of each app to change your passwords as you add them to ensure every password you use is different and secure.

## MFA

**Multi-factor authentication** is a method of accessing your accounts whereby you need multiple factors of authentication: typically a combination of something you know (such as a password), something you hold (such as a device or card) and/or something about you (such as fingerprints or iris etc.).

**Two-factor authentication** (commonly called 2FA) is the most common form of multi-factor authentication and is supported on a large number of online services.

Some time ago two-factor authentication for online services typically used a physical fob/token to generate a one-time password but there were many downsides including expense, delayed access and portability.

These days two-factor authentication usually consists of a free app running on a smartphone which generates a one-time password above which you enter in addition to your regular password to log onto a site or service.

I originally used [Google Authenticator](https://en.wikipedia.org/wiki/Google_Authenticator) for these but I have since moved to [Authy](https://www.authy.com/) on iOS because, as of a few months ago at least, Google Authenticator provides no convenient mechanism to move codes across devices (besides disabling and reenabling 2FA for every site you use).

Some sites also allow you to use SMS for two-factor authentication, but this may be less convenient if for example you're travelling in a different country using a different SIM card and don't have easy access to your SMS that you specified for your account.

Some password managers also allow you to generate one-time passwords like LastPass and 1Password. I prefer to keep my one-time passwords separate from my regular passwords.

Sites that use multi factor authentication allow you to generate and print backup codes in case you can't access your device. You can print and store these securely, but **you should never store these in your password vault** as this defeats the purpose of having multi-factor authentication since these codes bypass your multi factor authentication.

**You should enable multi-factor for any site that you use that supports it**. [WordPress.com](https://WordPress.com), Google, Github and Slack all support two-factor authentication. You can look up to see which online services support it on this [handy](https://twofactorauth.org/) website.

Some further reading [here](https://pixelprivacy.com/resources/two-factor-authentication/)

## Other

**Computers**

- Encrypt the contents of your computers. Mac OSX has File Vault in built in. I don't use Windows but I see [Windows 10 now has BitLocker built in](https://support.microsoft.com/en-us/instantanswers/e7d75dd2-29c2-16ac-f03d-20cfdf54202f/turn-on-device-encryption).
- Set a long pass-phrase style (rememberable) password for your computers.
- Have a password protected screen saver start within 15 mins or less of inactivity on your computer, and set up a shortcut to quickly lock your computer.
- Install/activate anti-virus: Windows 8 and up has Windows Defender in built, [Avira](https://www.avira.com/en/download-start-new/product/avira-free-mac-security) is a good option for OSX.
- Enable your firewall.

**Devices**

- Set at least an 8 digit pin or strong password for your phone/iPad (iOS supports these as custom length pins).
- Don't use a pattern to unlock your device.
- Ensure your Android device has encryption enabled.
- Enable iOS Find my iPhone, or Android Device Manager to locate and remotely wipe your phone.

**Home**

- Make sure your home router firmware is current and you aren't using the default password.
- Set a strong WPA2 passphrase password for your wireless network.
- Buy a document shredder and shred any bill, letter, document or boarding pass you are getting rid of -- boarding passes contain a s[urprising amount of personal information](http://www.inc.com/will-yakowicz/hackers-can-use-boarding-pass-barcode-to-swipe-personal-info.html) about you so be careful sharing photos of your boarding passes on social media.
