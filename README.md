# Build an offline, airgapped Bitcoin signing device for less than $50!

![Image of SeedSigners in Open Pill Enclosures](docs/img/Open_Pill_Star.JPG)![Image of SeedSigner in an Orange Pill enclosure](docs/img/Orange_Pill.JPG)

---------------

* [Project Summary](#project-summary)
* [Shopping List](#shopping-list)
* [Software Installation](#software-installation)
  * [Verifying the Software](#verifying-the-software)
* [Enclosure Designs](#enclosure-designs)
* [SeedQR Printable Templates](#seedqr-printable-templates)
* [Manual Installation Instructions](#manual-installation-instructions)


---------------

# Project Summary

The goal of SeedSigner is to lower the cost and complexity of Bitcoin multi-signature wallet use. To accomplish this goal, SeedSigner offers anyone the opportunity to build a verifiably air-gapped, stateless Bitcoin signing device using inexpensive, publicly available hardware components (usually < $50). SeedSigner helps users save with Bitcoin by assisting with trustless private key generation and multi-signature wallet setup, and helps users transact with Bitcoin via a secure, air-gapped QR-exchange signing model.

Additional information about the project can be found at [seedsigner.com](https://seedsigner.com).

You can follow [@SeedSigner](https://twitter.com/SeedSigner) on Twitter for the latest project news and developments.

If you have specific questions about the project, our [Telegram Group](https://t.me/joinchat/GHNuc_nhNQjLPWsS) is a great place to ask them.

### Feature Highlights:
* Calculate word 12/24 of a BIP39 seed phrase
* Create a 24-word BIP39 seed phrase with 99 dice rolls
* Create a 24-word BIP39 seed phrase by taking a digital photo 
* Temporarily store up to 3 seed phrases while device is powered
* Guided interface to manually create a SeedQR for instant input [(demo video here)](https://youtu.be/c1-PqTNx1vc)
* BIP39 passphrase / word 25 support
* Native Segwit Multisig XPUB generation w/ QR display
* Scan and parse transaction data from animated QR codes
* Sign transactions & transfer XPUB data using animated QR codes [(demo video here)](https://youtu.be/LPqvdQ2gSzs)
* Live preview during photo-to-seed and QR scanning UX
* Optimized seed word entry interface
* Support for Bitcoin Mainnet & Testnet
* Support for custom user-defined derivation paths
* On-demand receive address verification
* User-configurable QR code display density
* Responsive, event-driven user interface

### Considerations:
* Built for compatibility with Specter Desktop, Sparrow, and BlueWallet Vaults
* Device takes up to 60 seconds to boot before menu appears (be patient!)
* Always test your setup before transferring larger amounts of bitcoin (try Testnet first!)
* Taproot not quite yet supported
* Slightly rotating the screen clockwise or counter-clockwise should resolve lighting/glare issues
* If you think SeedSigner adds value to the Bitcoin ecosystem, please help us spread the word! (tweets, pics, videos, etc.)

### Planned Upcoming Improvements / Functionality:
* Single-sig and multi-sig change address verification
* Re-imagined, graphically-focused user interface
* Multi-language support
* Customized Linux live-boot OS to allow MicroSD card removal
* Other optimizations based on user feedback!

---------------

# Shopping List

To build a SeedSigner, you will need:

* Raspberry Pi Zero (preferably version 1.3 with no WiFi/Bluetooth capability, but any Raspberry Pi 2/3/4 or Zero model will work, Raspberry Pi 1 devices will require a hardware modification to the Waveshare LCD Hat, as per the [instructions here](./docs/legacy_hardware.md))
* Waveshare 1.3" 240x240 pxl LCD (correct pixel count is important, more info at https://www.waveshare.com/wiki/1.3inch_LCD_HAT)
* Pi Zero-compatible camera (tested to work with the Aokin / AuviPal 5MP 1080p with OV5647 Sensor)

Notes:
* You will need to solder the 40 GPIO pins (20 pins per row) to the Raspberry Pi Zero board. If you don't want to solder, purchase "GPIO Hammer Headers" for a solderless experience.
* Other cameras with the above sensor module should work, but may not fit in the Orange Pill enclosure
* Choose the Waveshare screen carefully; make sure to purchase the model that has a resolution of 240x240 pixels

---------------

# Software Installation

## A Special Note on Minimizing Trust
As is the nature of pre-packaged software downloads, downloading and using the prepared SeedSigner release images means implicitly placing trust in the individual preparing those images; in our project the release images are prepared and signed by the eponymous creator of the project, SeedSigner "the person". That individual is additionally the only person in possession of the PGP keys that are used to sign the release images.

However, one of the many advantages of the open source software model is that the need for this kind of trust can be negated by our users' ability to (1) review the project's source code and (2) assemble the operating image necessary to use the software themselves. From our project's inception, instructions to build a SeedSigner operating image (using precisely the same process that is used to create the prepared release images) have been made availabile. We have put a lot of thought and work into making these instructions easy to understand and follow, even for less technical users. These instructions can be found [here](docs/manual_installation.md).

## Downloading the Software

The quickest and easiest way to install the software is to download the most recent "seedsigner_X_X_X.zip" file in the [software releases](https://github.com/SeedSigner/seedsigner/releases) section of this repository.

After downloading the .zip file, verify it, extract the seedsigner .img file, and write it to a MicroSD card (at least 4GB in size or larger). Then install the MicroSD in the assembled hardware and off you go.
More detailed instructions to do these step are below. 

- Verify the digital signature of the software download to ensure that it is genuine and unchanged (optional, but recommended).
- Extract the SeedSigner.img file, and write it onto your MicroSD card (minimum 4GB in size).
- Insert the MicroSD into the assembled hardware and turn on the power!    

Note: If you require a more trustless installation by building from the  source code, you should follow these [manual installation instructions](docs/manual_installation.md).
<br>
<br>

# Verifying your downloaded files (optional, but recommended!)
You can quickly and easily verify that your downloaded software is both genuine and also unaltered, by following these instructions 

The 3 files you will need are all available [here](https://github.com/SeedSigner/seedsigner/releases), under the *Assets* heading.
1. seedsigner_0_5_x.img.zip 
2. seedsigner_0_5_x.img.zip.sha256 
3. seedsigner_0_5_x.img.zip.sha256.sig 

**Note:** The version numbers of the files might not match the above examples, but the naming format will be the same.  
This process assumes you are running the commands from a computer where both [GPG](https://gnupg.org/download/index.html) and [shasum](https://command-not-found.com/shasum) are already installed, that you know [how to navigate on a terminal](https://terminalcheatsheet.com/guides/navigate-terminal) and are already positioned in the same folder where you have saved the 3 files.   
(Which will most likely be your Downloads folder.)
<br>
<br>
## Importing the public key of the SeedSigner Project  
The first step is to import the *public key* of the SeedSigner project into your computers own *keychain*. The *fetch-keys*  command shown below will fetch the SeedSigner projects public key from a popular online keyserver called *Keybase.io*.  After the key is imported successfully, we will visually compare its properties to various websites to confirm it is genuine.   
Run this command:
```
gpg --fetch-keys https://keybase.io/SeedSigner/pgp_keys.asc
```
When  the command completes successfully, it will display a numeric ID, as circled in red in the example below. We will use that numeric ID in the next step.

![SS - Keybase PubKey import with Fingerprint shown (New import or update of the key)](https://user-images.githubusercontent.com/91296549/174248861-7961c038-1fbf-47a1-a110-146cb218b1c8.jpg)  
   
Now open the website <a href="https://www.Keybase.io/SeedSigner" target="_blank">KeyBase.io/SeedSigner</a> (it opens in a separate tab or window)

![SS - Keybase PubKey Verification via visual fingerprint matching3-50pct](https://user-images.githubusercontent.com/91296549/174390488-28f3e5af-dfe7-47d7-b69c-54971a00db17.jpg)

These numeric IDs are known as the keys *fingerprint*, and now you will now visually compare them to make sure that the *imported* fingerprint and the *website* fingerprint match exactly. You should ignore the white spaces, which are just there to help readability. 

If the 2 fingerprints are an exact match, then this means that the public key that you have just imported, does genuinely belong to the SeedSigner project.  You have now confirmed know *who* the public key belongs to!  
In the next step, you will make certain that this *same* key was used to sign your downloaded files.  

<details><summary> Expand this section if you are curious about what the 2 matching fingerprints prove and what they do.</summary>     

The Keybase.io website has a unique ability to *cryptographically* confirm that the public key specified is *actually from the same people* who manage all of Seedsigner's online presence! 

Keybase.io does this by requesting some "social proofs" of the Seedsigner project's [human] leaders. By completing these specific tasks online, the humans prove *that they are who they say they are*, online. 
(Much like how  Satoshi could prove that they are __real__ Satoshi, by moving a single bitcoin from the known Satoshi wallet.) 
<br>
Keybase's magic is achieved by asking the Seedsigner Project's leaders to announce their ownership of their public key in all of their online channels, and then prove cryptographically that it was really done. This proof is done across (2 or more) of their known online or social media channels,  eg the project website (seedsigner.com), their Twitter account (@seedsigner) and their GitHub account (github.com/seedsigner). Keybase will then confirm, -cryptographically-, that they did in fact manage to do the tasks exactly as instructed, and hence it confirms that *they are who they say they are.*  
Keybase then continues to periodically check the public proof that this key is still from them.
</details>  

<br> 

## Verifying that your download is genuine 
 
The next steps will show you how to confirm that your downloaded .zip file is the genuine and unaltered SeedSigner software.  
You will achieve this by electronically comparing the *hash* value of *your* zip file to the *original* zip file’s hash value, and also use  the public/private key pair cryptographic signatures. 

The two steps are:  
1.	Determine *who* signed the sha256.sig file which you downloaded earlier.  
To establish this, the GPG *verify* command will used.  
The *verify* command loops through all the public keys on your computer and identifies *which* key pair signed your sha256.sig file, by comparing it (cryptographically) to its unsigned equivalent (your .sha256 file).  
The verify command outputs the all-important *signers* fingerprint, which is what you will visually compare to the fingerprint you previously found on Keybase.io/SeedSigner.  
That step completes the three cross-checks on this fingerprint!  

2.	Lastly, you will use the *shasum* command to generate (and compare) the hash value of your *downloaded* Zip file to the hash value of the *original* Zip file (as noted inside of the .SHA256 plaintext file).  
If the 2 *hashes* match, then your downloaded zip file is **safe for use**, because it is now confirmed as the one that was signed the SeedSigner project team and is also confirmed as unaltered (in transit and at rest)!  



**Step one:**      Run the *verify* command :  
```
gpg --verify seedsigner_0_*_*.img.zip.sha256.sig
```
**Note:** The `*`s in the command will auto-match to the version number in your current folder. It should be copied and pasted as-is.


The response **must** include the phrase **"Good signature"**, like this: 

>Good signature from "seedsigner <btc.hardware.solutions @ gmail.com>" [unknown]  

The email address is just informational. *Only* the matching fingerprints count.   
<br>
If the response displays "BAD signature", then you must stop here immediately and contact us for assistance.  

This warning message below, is normal however.

> gpg: WARNING: This key is not certified with a trusted signature!  
> gpg:          There is no indication that the signature belongs to the owner.

The last line will display a key fingerprint, which is the all-important number which you will now visually compare to the one on Keybase.io/SeedSigner.   
That step completes the three cross-checks on this fingerprint!   
<br>
If it does not match exactly, then  stop here immediately and contact us for  assistance.
<br>
<br>

**Step Two:**  Run the *shasum* command : <br>
**On Linux or OSX**
```
shasum -a 256 -c seedsigner_0_*_*.img.zip.sha256
```

**Windows**
```
CertUtil -hashfile  seedsigner_0_*_*.img.zip SHA256 | findstr /v "hash"
```

The response must include the text **seedsigner_[VersionNumber].img.zip OK**, like this:   
```
seedsigner_0_5_x.img.zip: OK
```

The **OK** result means that 2 hashes are an exact match, and thus your zip file is **safe for use**.  It is has been successfully verified as both genuinely produced by the SeedSigner project team themselves and also not altered in any way.   
If the output does **not** show "OK", then immediately stop here and ask for assistance!   

**Verification Succeded!!  - well done, your zip file is now confirmed as authentic**!   
<br>
## Write the software to the MicroSD card 
You can now extract the zip file contents, and write them to your MicroSD card.  
We recommend using the Balena Etcher or Pi Imager applications to do this. Utilizing  their 'verify after writing' option is **highly recommended** to make sure the file was written out successfully, and avoid any MicroSD writing issues.   
When that is complete, simply insert the MicroSD card (pin side down) into your SeedSigner and apply electrical power from your usb adapter. It is not recommended to use usb ports from a computer, as this will break the air-gap around your seedsigner.

The seedsigner can take up to 45 seconds to show its opening screen, however you should see the led light on the circuit board inside flickering throughtout the boot-up sequence. 
<br>

There are other steps you can take to verify the software, including examining the hash value in the .sha256 text file, but this one has been documented here because it seems the simplest for most people to follow. Please recognize that this process can only validate the software to the extent that the entity that first published the key is an honest actor, and assumes the private key has remained uncompromised and is not being used by a malicious actor. 

<br> 
---------------

# Enclosure Designs

### Open Pill

The Open Pill enclosure design is all about quick, simple and inexpensive depoloyment of a SeedSigner device. The design does not require any additional hardware and can be printed using a standard FDM 3D printer in about 2 hours, no supports necessary. A video demonstrating the assembly process can be found [here](https://youtu.be/gXPFJygZobEa). To access the design file and printable model, click [here](https://github.com/SeedSigner/seedsigner/tree/main/enclosures/open_pill).

### Orange Pill

The Orange Pill enclosure design offers a more finished look that includes button covers and a joystick topper. You'll also need the following additional hardware to assemble it:

* 4 x F-F M2.5 spacers, 10mm length
* 4 x M2.5 pan head screws, 6mm length
* 4 x M2.5 pan head screws, 12mm length

The upper and lower portions of the enclosure can be printed using a standard FDM 3D printer, no supports necessary. The buttons and joystick nub should ideally be produced with a SLA/resin printer. An overview of the entire assembly process can be found [here](https://youtu.be/aIIc2DiZYcI). To access the design files and printable models, click [here](https://github.com/SeedSigner/seedsigner/tree/main/enclosures/orange_pill).

### Community Designs

* [Lil Pill](https://cults3d.com/en/3d-model/gadget/lil-pill-seedsigner-case) by @_CyberNomad
* [OrangeSurf Case](https://github.com/orangesurf/orangesurf-seedsigner-case) by @OrangeSurfBTC
* [PS4 Seedsigner](https://www.thingiverse.com/thing:5363525) by @Silexperience
* [OpenPill Faceplate](https://www.printables.com/en/model/179924-seedsigner-open-pill-cover-plates-digital-cross-jo) by @Revetuzo 
* [Waveshare CoverPlate](https://cults3d.com/en/3d-model/various/seedsigner-coverplate-for-waveshare-1-3-inch-lcd-hat-with-240x240-pixel-display) by @Adathome1

---------------

# SeedQR Printable Templates
You can use SeedSigner to export your seed to a hand-transcribed SeedQR format that enables you to instantly load your seed back into SeedSigner.

[More information about SeedQRs](docs/seed_qr/README.md)

<table align="center">
    <tr><td><img src="docs/seed_qr/img/handmade_qr.jpg"></td></tr>
</table>

Standard SeedQR templates:
* [12-word SeedQR template (25x25)](docs/seed_qr/printable_templates/12words_seedqr_template.pdf)
* [24-word SeedQR template (29x29)](docs/seed_qr/printable_templates/24words_seedqr_template.pdf)
* [Baseball card template: 24-word SeedQR (29x29)](docs/seed_qr/printable_templates/Seed_QR_Card.pdf)

CompactSeedQR templates:
* [12-word CompactSeedQR template (21x21)](docs/seed_qr/printable_templates/compact_seedqr/12words_compactseedqr_template.pdf)
* [24-word CompactSeedQR template (25x25)](docs/seed_qr/printable_templates/compact_seedqr/24words_compactseedqr_template.pdf)

_note: CompactSeedQR is an advanced feature that can be enabled in Settings_

---------------

# Manual Installation Instructions
see the docs: [Manual Installation Instructions](docs/manual_installation.md)
