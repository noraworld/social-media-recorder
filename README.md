# Social Media Recorder
Social Media Recorder is a repository where my posts on several social media are integrated with [my diary](https://github.com/noraworld/diary). Even though this is my personal repository, you can establish a similar structure by following the instructions provided below.

## Setup
Every time something is posted from my accounts on social media, it is transferred to this repository. Each comment posted on [Issue #1](https://github.com/noraworld/social-media-recorder/issues/1) is moved to the latest issue on [my diary repository](https://github.com/noraworld/diary) automatically. Here's how to setup like that.

```mermaid
flowchart LR
    social_media(Social media#13;#40;Twitter, Mastodon, etc.#41;) --> social_media_recorder(Social Media Recorder#13;#40;this repository#41;) --> my_diary(My diary#13;#40;another repository#41;)
```

### IFTTT
[IFTTT](https://ifttt.com) is used here as it's way cheaper than subscribing to [the X (Twitter) API](https://developer.x.com/en/docs/x-api).

#### Upgrade plan
You need to upgrade your IFTTT account to [Pro or Pro+](https://ifttt.com/plans) to use the Twitter trigger "New tweet by you".

#### Register applets
Create your applets by following the instructions provided below.

##### Twitter
###### Trigger
| Field           | Value                                                  |
| --------------- | ------------------------------------------------------ |
| Twitter account | Your Twitter account information associated with IFTTT |
| retweets        | unchecked                                              |
| @replies        | unchecked                                              |

<img src="assets/twitter_trigger.png?raw=true" width="70%">

###### Action
| Field           | Value                                                 |
| --------------- | ----------------------------------------------------- |
| GitHub account  | Your GitHub account information associated with IFTTT |
| Repository Name | `noraworld/social-media-recorder`                     |
| Issue Number    | `1`                                                   |
| Comment         | See below                                             |

```
{{Text}}

> From [Twitter]({{LinkToTweet}}) on {{CreatedAt}}
```

<img src="assets/twitter_action.png?raw=true" width="70%">

##### Mastodon
###### Trigger
| Field                   | Value                                                          |
| ----------------------- | -------------------------------------------------------------- |
| Mastodon.social account | Your Mastodon.social account information associated with IFTTT |

<img src="assets/mastodon_trigger.png?raw=true" width="70%">

###### Action
| Field           | Value                                                 |
| --------------- | ----------------------------------------------------- |
| GitHub account  | Your GitHub account information associated with IFTTT |
| Repository Name | `noraworld/social-media-recorder`                     |
| Issue Number    | `1`                                                   |
| Comment         | See below                                             |

```
{{ContentHtml}}

![]({{MediaUrl}})

> From [Mastodon]({{Url}}) on {{CreatedAt}}
```

<img src="assets/mastodon_action.png?raw=true" width="70%">

##### Misskey
###### Trigger
| Field              | Value                                                     |
| ------------------ | --------------------------------------------------------- |
| Misskey.io account | Your Misskey.io account information associated with IFTTT |

<img src="assets/misskey_trigger.png?raw=true" width="70%">

###### Action
| Field           | Value                                                 |
| --------------- | ----------------------------------------------------- |
| GitHub account  | Your GitHub account information associated with IFTTT |
| Repository Name | `noraworld/social-media-recorder`                     |
| Issue Number    | `1`                                                   |
| Comment         | See below                                             |

```
{{EntryContent}}

![]({{EntryImageUrl}})

> From [Misskey]({{EntryUrl}}) on {{EntryPublished}}
```

<img src="assets/misskey_action.png?raw=true" width="70%">

### Create workflow
Create a workflow by following [`comments-transferor.yml`](.github/workflows/comments-transferor.yml).

### Lock conversation
You should lock the conversation on [Issue #1](https://github.com/noraworld/social-media-recorder/issues/1) so that no one can post a comment here. Otherwise, someone's comment will be transferred to your another repository.

```shell
gh issue lock --repo noraworld/social-media-recorder 1
```

## Expected questions
### Why don't you specify directly on IFTTT which issue the posts will be shared with?
Because IFTTT doesn't provide the option to specify the latest GitHub issue. You have to specify a static issue number, which means the special variable or programmatic way is not available.

### Why don't you turn this repository private if you are concerned that someone posts a comment here?
Because there is no limit to running workflows for public repositories! If it is possible to guarantee that nobody can play a trick and post a useless comment on purpose, free and no limit options are better, aren't they?
