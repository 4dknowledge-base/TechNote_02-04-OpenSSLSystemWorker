# Installation

The demonstration 4D application to this technical note ensures cross-platform compatibility and was developed for both Windows and macOS operating systems. To achieve this cross-platform functionality, the system implements dynamic detection of the OpenSSL binary path, automatically locating the executable in the default installation path for each respective platform. This automatic detection significantly reduces configuration complexity for end users while still maintaining flexibility for custom installations. If OpenSSL exists in a non-standard folder location, the application provides a mechanism for users to manually specify the executable path, which is then stored in the application session and used for all subsequent operations.

This tech note was produced in the following context: &#8211; 4D 21 LTS (https://us.4d.com/product-download/4D-21-LTS)

&#8211; OpenSSL version 3.0 or later

&#8211; Windows 11 – macOS Tahoe 26 (Apple Silicon)