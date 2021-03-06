# SwifterSockets
A collection of socket utilities in pure Swift

SwifterSockets is part of [Swiftfire](http://swiftfire.nl), the server for websites build with Swift.

# Features
- Shields the Swift application from the complexity of the Unix socket calls.
- Directly interfaces with the POSIX calls using:
	- connectToTipServer
	- tipTransfer
	- tipReceiverLoop
	- tipAccept
	- setupTipServer
- Implements a framework on top of the POSIX calls with:
	- Connection (class)
	- connectToTipServer (returns a connection)
	- TipServer (class, produces connections)
- Includes replacements for the FD_SET, FD_CLR, FD_ZERO and FD_ISSET macro's.
- Builds as a library using the Swift Package Manager (SPM)

# Tip

If you need secure connections, check out [SecureSockets](https://github.com/Balancingrock/SecureSockets). SecureSockets is build on top of SwifterSockets (and OpenSSL).

# Reference manual

The reference manual is hosted at [Swiftfire.nl](http://swiftfire.nl/projects/swiftersockets/reference/index.html)

# Installation

SwifterSockets is distributed as a Swift package and as a framework.

## Use as a SPM package

Extend the dependency of your project package with:

    dependencies: [
        ...
        .Package(url: "https://github.com/Balancingrock/SwifterSockets", <version-number>)
    ]

The _<version-number>_ must be replaced with the version number that must be used, for example: "0.2.0".

## Use as a framework

First clone SwifterSockets and the create the Xcode project:

At the command line:

    $ git clone https://github.com/Balancingrock/SwifterSockets
    $ cd SwifterSockets
    $ swift package generate-xcodeproj

Double click that project to open it. Once open set the `Defines Module` to 'yes' in the `Build Settings` before creating the framework. (Otherwise the import of the framework in another project won't work)

In the project that will use SwifterSockets, add the SwifterSockets.framework by opening the `General` settings of the target and add the SwifterSockets.framework to the `Embedded Binaries`.

In the Swift source code import SwifterSockets by "import SwifterSockets" at the top of the file.

# Version history

Note: Planned releases are for information only, they are subject to change without notice.

#### 1.1.0 (Open)

- No new features planned. Features and bugfixes will be made on an ad-hoc basis as needed to support Swiftfire development.
- For feature requests and bugfixes please contact rien@balancingrock.nl

#### 1.0.0 (Planned)

- The current verion will be upgraded to 1.0.0 status when the full set necessary for Swiftfire 1.0.0 has been completed.

#### 0.10.9 (Current)

- Upgraded BRUtils to 0.9.0

#### 0.10.8

- Upgraded BRUtils to 0.5.0
- Made incrementUsageCount and decrementUsageCount public.

#### 0.10.7

- Bugfix: Closing a connection of a connection object could crash an application (rare, only observed once).
- Bugfix: There was a conditon that would prevent the release of connection objects causing a server to run out of connection objects (common when a server ran for several days without restarts)

#### 0.10.6

- Updated the references captured by closures.
- In transmitterClosed the inerface is immediately set to 'nil' to prevent errors in an SSL connectionon closing.
- Renamed 'abortConnection' to 'connectionWasClosed'.
- Added sorting to the connection pool.
- Added closing of the socket on transmitterClosed.

#### 0.10.5

- Added affectInactivityDetection parameter (default = true) to the transfer calls.

#### 0.10.4

- Bugfix: The sQueue in SwifterSocket.Connection could be deallocated before its processes were complete.

#### 0.10.3

- BRUtils update to 0.2.0

#### 0.10.2 

- Moved Result type to BRUtils

#### 0.10.1

- Compile time improvement

#### v0.10.0

- Added a result function to process Result<T> results
 
#### 0.9.15

- Added inactivity detection for Connections.

#### 0.9.14

- More access level updates
- Added buffer pointer to transfer protocol
- Added buffered transmissions to Connections
- Moved some protocols from the general area to specific files
- Added connection pool manager

#### 0.9.13

- Re-evaluated open/public access
- Added logId fo the InterfaceAccess protocol
- Updated comments

#### 0.9.12

- Improved documentation for reference manual generation

#### 0.9.11

- Comment changes
 
#### 0.9.10

- Added xcode project for framework generation

#### 0.9.9

- Fixed some access control levels

#### 0.9.8

- Major redesign to support SecureSockets the SSL complement to SwifterSockets. The old interfaces have changed and the thread related operations have been replaced by the new approach to use Connection objects rather than directly interfacing with the threads.

#### 0.9.7

- Upgraded to Xcode 8 beta 6 (Swift 3)

#### 0.9.6

- Upgraded to Xcode 8 beta 3 (swift 3)

#### 0.9.5

- Fixed a bug where accepting an IPv6 connection would fill an IPv4 sockaddr structure.
- Added SocketAddress enum adopted from Marco Masser: http://blog.obdev.at/representing-socket-addresses-in-swift-using-enums

#### 0.9.4

- Header update to include new website: [swiftfire.nl](http://swiftfire.nl)

#### 0.9.3

- Changed target to framework
- Made the necessary interfaces public
- Removed the dependency on SwifterLog to prevent cross-usage
- Added tags to mark releases
- Removed other not used files/directories

#### 0.9.2

- Upgraded to Swift 2.2.
- Added closeSocket call.
- Added 'logUnixSocketCalls' (needs [SwifterLog](https://github.com/Swiftrien/SwifterLog)).
- Added note on buffer capture to transmitAsync:buffer.
- Added SERVER_CLOSED and CLIENT_CLOSED to TransmitResult.
- Changed DataEndDetector from a class to a protocol.
- Added SERVER_CLOSED to ReceiveResult.
- Replaced error numbers in the receiver functions with #file.#function.#line
- Added CLOSED AcceptResult.
- Fixed a bug that missed the error return from the select call in the accept functions.


#### 0.9.1

- Changed type of object in 'synchronized' from AnyObject to NSObject
- Added EXC_BAD_INSTRUCTION info to fd_set
- TransmitTelemetry and ReceiveTelemetry now inherit from NSObject
- Replaced (UnsafePointer<UInt8>, length) with UnsafeBufferPointer<UInt8>
- Added note on DataEndDetector that it can be used to receive the data also.

#### 0.9.0

- Initial release
