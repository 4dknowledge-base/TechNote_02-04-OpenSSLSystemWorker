# OpenSSL in 4D using System Workers

In the modern landscape of digital security, the ability to generate, manage, and utilize cryptographic assets such as private keys, Certificate Signing Requests (CSR), and signed certificates and documents are no longer an optional feature; it is a fundamental requirement for compliance, e-invoicing, and secure data exchange. Organizations operating in regulated industries face strict mandates regarding data security and identity verification, making robust cryptographic infrastructure essential for business operations. Furthermore, the increasing prevalence of electronic invoicing systems and supply chain automation has created a need for developers to implement sophisticated digital signature mechanisms that can verify the authenticity and integrity of transmitted data.

This document serves as a comprehensive technical manual for integrating OpenSSL within the 4D development environment using the 4D.SystemWorker class. By moving away from legacy synchronous execution patterns with LAUNCH EXTERNAL PROCESS that block application threads and embracing the asynchronous capabilities of System Workers, developers can build responsive, high-performance applications that interact directly with the operating system&#8217;s command-line interface. The asynchronous approach represents a significant architectural evolution, allowing cryptographic operations to execute in the background while the main application thread remains available to process user interactions and handle other concurrent tasks. This transition from blocking to non-blocking execution is particularly important for applications that must maintain responsiveness during certificate generation, which can take several seconds or even minutes depending on key size and system resources.

## System Requirements

The demonstration 4D application to this technical note ensures cross-platform compatibility and was developed for both Windows and macOS operating systems. To achieve this cross-platform functionality, the system implements dynamic detection of the OpenSSL binary path, automatically locating the executable in the default installation path for each respective platform. This automatic detection significantly reduces configuration complexity for end users while still maintaining flexibility for custom installations. If OpenSSL exists in a non-standard folder location, the application provides a mechanism for users to manually specify the executable path, which is then stored in the application session and used for all subsequent operations.

This tech note was produced in the following context: &#8211; 4D 21 LTS ([https://us.4d.com/product-download/4D-21-LTS](https://us.4d.com/product-download/4D-21-LTS))

&#8211; OpenSSL version 3.0 or later

&#8211; Windows 11 – macOS Tahoe 26 (Apple Silicon)

OpenSSL Installation For developers who do not yet have OpenSSL installed on the development machines, the installation process is straightforward on both supported platforms.

### Windows Installation

Windows users can leverage the Windows Package Manager by executing winget install openssl from a command prompt or PowerShell window, which automatically downloads and installs the latest stable version of OpenSSL along with all necessary dependencies.

```4d
winget upgrade

winget install openssl

winget search openssl
```

### MacOS Installation

macOS users can utilize Homebrew, the popular package manager for macOS in the Terminal application.

```4d
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

brew install openssl
```

In the demonstration application, the user can check if OpenSSL was successfully installed thanks to the OpenSSL system check form.

```4d
var $i : Integer

ALL RECORDS([Table_2])
If (Records in selection([Table_2])=0)
	For ($i; 1; 20)
		
		CREATE RECORD([Table_2])
		
		[Table_2]Field_2:="Record "+String($i)
		
		SAVE RECORD([Table_2])
		
	End for 
End if
```

## Downloadable Materials

The following materials are available for download:

- <a href="https://preprod-learn.4d.com/wp-content/uploads/2026/04/TN-OpenSSL-3.zip" target="_blank">Demo Project OpenSSL</a>
- <a href="https://github.com/4dknowledge-base/TechNote_02-04-OpenSSLSystemWorker" target="_blank">Github Repo</a>
