# Social Media Recorder
Social Media Recorder is a repository where my posts on several social media are integrated with [my diary](https://github.com/noraworld/diary). Even though this is my personal repository, you can establish a similar structure by following the instructions provided below.

## Setup
Each comment posted on [Issue #1](https://github.com/noraworld/social-media-recorder/issues/1) is moved to the latest issue on my diary repository automatically. Here's how to setup like that.

### IFTTT
[IFTTT](https://ifttt.com) is used here as it's way cheaper than subscribing to [the X (Twitter) API](https://developer.x.com/en/docs/x-api).

#### Twitter
##### Trigger
| Field           | Value                                                  |
| --------------- | ------------------------------------------------------ |
| Twitter account | Your Twitter account information associated with IFTTT |
| retweets        | unchecked                                              |
| @replies        | unchecked                                              |

<img src="assets/twitter_trigger.png?raw=true" width="70%">

##### Action
| Field           | Value                                                 |
| --------------- | ----------------------------------------------------- |
| GitHub account  | Your GitHub account information associated with IFTTT |
| Repository Name | `noraworld/social-media-recorder`                     |
| Issue Number    | `1`                                                   |
| Comment         | See below                                             |

```
{{Text}}

> From [Twitter]({{LinkToTweet}})
```

<img src="assets/twitter_action.png?raw=true" width="70%">

#### Mastodon
##### Trigger
| Field                   | Value                                                          |
| ----------------------- | -------------------------------------------------------------- |
| Mastodon.social account | Your Mastodon.social account information associated with IFTTT |

<img src="assets/mastodon_trigger.png?raw=true" width="70%">

##### Action
| Field           | Value                                                 |
| --------------- | ----------------------------------------------------- |
| GitHub account  | Your GitHub account information associated with IFTTT |
| Repository Name | `noraworld/social-media-recorder`                     |
| Issue Number    | `1`                                                   |
| Comment         | See below                                             |

```
{{ContentHtml}}

![]({{MediaUrl}})

> From [Mastodon]({{Url}})
```

<img src="assets/mastodon_action.png?raw=true" width="70%">

### Lock conversation
You should lock the conversation on [Issue #1](https://github.com/noraworld/social-media-recorder/issues/1) so that no one can post a comment here. Otherwise, someone's comment will be transferred to my diary.

```shell
gh issue lock --repo noraworld/social-media-recorder 1
```
