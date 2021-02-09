## Welcome to ContainerRelease Page

### Name

container-release — Container system identification

### Synopsis
/etc/container-release

/usr/lib/container-release

### Description

The /etc/container-release and /usr/lib/container-release files contain container system identification data.

The basic file format of container-release is a newline-separated list of environment-like shell-compatible variable assignments. It is possible to source the configuration from shell scripts, however, beyond mere variable assignments, no shell features are supported (this means variable expansion is explicitly not supported), allowing applications to read the file without implementing a shell compatible execution engine. Variable assignment values must be enclosed in double or single quotes if they include spaces, semicolons or other special characters outside of A–Z, a–z, 0–9. Shell special characters ("$", quotes, backslash, backtick) must be escaped with backslashes, following shell style. All strings should be in UTF-8 format, and non-printable characters should not be used. It is not supported to concatenate multiple individually quoted strings. Lines beginning with "#" shall be ignored as comments. Blank lines are permitted and ignored.

The file /etc/container-release takes precedence over /usr/lib/container-release. Applications should check for the former, and exclusively use its data if it exists, and only fall back to /usr/lib/container-release if it is missing. Applications should not read data from both files at the same time. /usr/lib/container-release is the recommended place to store Container release information as part of vendor trees. /etc/container-release should be a relative symlink to /usr/lib/container-release, to provide compatibility with applications only looking at /etc/. A relative symlink instead of an absolute symlink is necessary to avoid breaking the link in a chroot or initrd environment such as dracut.

container-release contains data that is defined by the container image system vendor and should generally not be changed by the administrator.

As this file only encodes names and identifiers it should not be localized.

The /etc/container-release and /usr/lib/container-release files might be symlinks to other files, but it is important that the file is available from earliest boot on, and hence must be located on the root file system.

### Options

The following Container identifications parameters may be set using container-release:

NAME=
A string identifying the container image, without a version component, and suitable for presentation to the user. If not set, defaults to "NAME=Application". Example: "NAME=Nginx" or "NAME="Nginx/PHP"".

VERSION=
A string identifying the container image version, possibly including a release code name, and suitable for presentation to the user. This field is optional. Example: "VERSION=17" or "VERSION="17 (snapshot)"".

ID=
A lower-case string (no spaces or other characters outside of 0–9, a–z, ".", "_" and "-") identifying the operating system, excluding any version information and suitable for processing by scripts or usage in generated filenames. If not set, defaults to "ID=Container". Example: "ID=nginx" or "ID=apache".

VERSION_CODENAME=
A lower-case string (no spaces or other characters outside of 0–9, a–z, ".", "_" and "-") identifying the container system release code name, and suitable for processing by scripts or usage in generated filenames. This field is optional and may not be implemented on all images. Examples: "VERSION_CODENAME=daydream", "VERSION_CODENAME=xenial"

VERSION_ID=
A lower-case string (mostly numeric, no spaces or other characters outside of 0–9, a–z, ".", "_" and "-") identifying the image version, and suitable for processing by scripts or usage in generated filenames. This field is optional. Example: "VERSION_ID=17" or "VERSION_ID=11.04".

PRETTY_NAME=
A pretty image system name in a format suitable for presentation to the user. May or may not contain a release code name or image version of some kind, as suitable. If not set, defaults to "PRETTY_NAME="Nginx"". Example: "PRETTY_NAME="Apache 17 (Daydream)"".

HOME_URL=, DOCUMENTATION_URL=, SUPPORT_URL=, BUG_REPORT_URL=, PRIVACY_POLICY_URL=
Links to resources on the Internet related to the image. HOME_URL= should refer to the homepage of the image, or alternatively some homepage of the specific version of the image. DOCUMENTATION_URL= should refer to the main documentation page. SUPPORT_URL= should refer to the main support page for the image, if there is any. This is primarily intended for images which vendors provide support for. BUG_REPORT_URL= should refer to the main bug reporting page for the image system, if there is any. This is primarily intended for images that rely on community QA. PRIVACY_POLICY_URL= should refer to the main privacy policy page for the image, if there is any. These settings are optional, and providing only some of these settings is common. These URLs are intended to be exposed in "About this image" UIs behind links with captions such as "About this Image", "Obtain Support", "Report a Bug", or "Privacy Policy". The values should be in RFC3986 format, and should be "http:" or "https:" URLs, and possibly "mailto:" or "tel:". Only one URL shall be listed in each setting. If multiple resources need to be referenced, it is recommended to provide an online landing page linking all available resources. Examples: "HOME_URL="https://docker.com/"" and "BUG_REPORT_URL="https://bugzilla.redhat.com/""

### Example
NAME=Nginx
VERSION="22 (Daydream)"
ID=nginx
VERSION_ID=22
PRETTY_NAME="Nginx 22 (Daydream)"
HOME_URL="https://nginx.com/"
DOCUMENTATION_URL="https://docs.nginx.com/"
SUPPORT_URL="https://nginx.com/support"
BUG_REPORT_URL="https://bugzilla.nginx.com/"
PRIVACY_POLICY_URL="https://nginx.com/PrivacyPolicy"



Based on [freedesktop.org/software/systemd/man/os-release.html](https://www.freedesktop.org/software/systemd/man/os-release.html)

