# messenger-api-python
[![PyPI](https://img.shields.io/pypi/v/messenger-api-python.svg?maxAge=2592000)](https://pypi.python.org/pypi/messenger-api-python)

Python Wrapper to various APIs from [Facebook Messenger Platform](https://developers.facebook.com/docs/messenger-platform).


## Features

### Send API (v16.0)
 - Send text messages
 - Send attachments from a remote file (image, audio, video, file)
 - Send attachments from a local file (image, audio, video, file)
 - Send templates (generic messages)
 - Send quick replies
 - Send buttons
### Profile API (v16.0)
- Set welcome screen
- Set persistent menu
### Attachment Upload API (v16.0)
- Upload attachments from a remote file (image, audio, video, file)
- Upload attachments from a local file (image, audio video, file)
### Reusable components
Various components used when sending messages in Facebook Messenger are wrapped into Python objects to make them reusable and easy to use.
- **Elements:** used to contains various Element objects
- **Element:** a card-like component that holds various other components
- **Buttons:** used to contains various Button objects
- **Button:** button used in various other components, can also be used alone
- **QuickReplies:** used to contains various QuickReply objects
- **QuickReply:** used when sending messages accompanied with quick replies
- **PersistentMenu:** used when setting up persistent menu

## Prerequisite
- **Python 3.7+** installed
- You'll need to setup a [Facebook App](https://developers.facebook.com/apps/), Facebook Page, get the Page Access Token and link the App to the Page.
## How to install
### From GitHub
```bash
pip install git+https://github.com/krishna2206/messenger-api-python.git#egg=messenger-api-python
```
### From Pypi
Package from Pypi.org may not be the latest one, if you want the latest version of this package, install it from the GitHub repository (see above)
```bash
pip install messenger-api-python
```
## Usage
### Send API
```python
from messengerapi import SendApi
send_api = SendApi(<page_access_token>)
send_api.send_text_message(<message>, <recipient_id>)
```
**Note**: From Facebook regarding User IDs

> These ids are page-scoped. These ids differ from those returned from Facebook Login apps which are app-scoped. You must use ids retrieved from a Messenger integration for this page in order to function properly.

##### Sending a generic template message:

> [Generic Template Messages](https://developers.facebook.com/docs/messenger-platform/implementation#receive_message) allows you to add cool elements like images, text all in a single bubble.
```python
from messengerapi import SendApi
from messengerapi.components import Elements, Element, Buttons, Button, POSTBACK

send_api = SendApi(<page_access_token>)

elements = Elements()
buttons = Buttons()

button = Button(button_type=POSTBACK, title="My button")
buttons.add_button(button.get_content())
element = Element(title="My element", subtitle="The element's subtitle, image_url=<image_url>, buttons=buttons)
elements.add_element(element.get_content())

send_api.send_generic_message(elements.get_content() , recipient_id , image_aspect_ratio="horizontal")
```
##### Sending remote (from URL) image/audio/video/file:
```python
from messengerapi import SendApi

send_api = SendApi(<page_access_token>)

# To send an image
send_api.send_image_attachment(<image_url> , <recipient_id>)
# To send an audio
send_api.send_audio_attachment(<audio_url> , <recipient_id>)
# To send a video
send_api.send_video_attachment(<video_url> , <recipient_id>)
# To send a file
send_api.send_file_attachment(<file_url> , <recipient_id>)
```
##### Sending local image/audio/video/file:
```python
from messengerapi import SendApi

send_api = SendApi(<page_access_token>)

# To send an image
send_api.send_local_image(<image_location> , <recipient_id>)
# To send an audio
send_api.send_local_audio(<audio_location> , <recipient_id>)
# To send a video
send_api.send_local_video(<video_location> , <recipient_id>)
# To send a file
send_api.send_local_file(<file_location> , <recipient_id>)
```## To do
- Securing requests


-   name: Setup Python
  uses: actions/setup-python@v4.7.1
  with:
    # Version range or exact version of Python or PyPy to use, using SemVer's version range syntax. Reads from .python-version if unset.
    python-version: # optional
    # File containing the Python version to use. Example: .python-version
    python-version-file: # optional
    # Used to specify a package manager for caching in the default directory. Supported values: pip, pipenv, poetry.
    cache: # optional
    # The target architecture (x86, x64) of the Python or PyPy interpreter.
    architecture: # optional
    # Set this option if you want the action to check for the latest available version that satisfies the version spec.
    check-latest: # optional
    # The token used to authenticate when fetching Python distributions from https://github.com/actions/python-versions. When running this action on github.com, the default value is sufficient. When running on GHES, you can pass a personal access token for github.com if you are experiencing rate limiting.
    token: # optional, default is ${{ github.server_url == 'https://github.com' && github.token || '' }}
    # Used to specify the path to dependency files. Supports wildcards or a list of file names for caching multiple dependencies.
    cache-dependency-path: # optional
    # Set this option if you want the action to update environment variables.
    update-environment: # optional, default is true
    # When 'true', a version range passed to 'python-version' input will match prerelease versions if no GA versions are found. Only 'x.y' version range is supported for CPython.
    allow-prereleases: # optional
