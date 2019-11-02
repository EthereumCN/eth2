# Two-Point-Oh

## The Explainers <a id="tip0"></a>

[![Join the chat at https://gitter.im/status-im/the-explainers](https://badges.gitter.im/status-im/the-explainers.svg)](https://gitter.im/status-im/the-explainers?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

![](https://raw.githubusercontent.com/status-im/the-explainers/master//header.png)

The Explainers Initiative is an open effort to bring technical content regarding the Serenity upgrade of the Ethereum blockchain closer to non-technical and semi-technical communities.

Inspired by the very successful [Peer Review at SitePoint](https://github.com/sitepoint-editors/php-peers) and [Bitfalls](https://github.com/sitepoint-editors/php-peers), the purpose of this repository is to be able to publicly draft Ethereum 2.0 content \(tutorials, explanations, guides\) and get feedback on in-progress posts by anyone who's interested - peer review style.

### What is peer review? <a id="tip1"></a>

Peer review is the process of peers \(those equal in knowledge and/or power\) providing constructive criticism on each other's content. Each article and each amendment to an article made by someone other than the author is a pull request itself. The feedback thus comes in the form of \(usually written\) comments or pull requests and comments on pull requests.

While this does present a barrier to non-technical contributors, this is on purpose. By approaching content as code and encouraging technical users to contribute in any way, we cover the widest possible range of interests and contexts but keep the qualifications of the pool of contributors largely intact.

### How do I join as reviewer/author? <a id="tip2"></a>

Note that no professional author will take _constructive_ criticism personally. However, given the amount of effort that can go into producing a good long-form post or tutorial, it's rare for people not to get emotionally attached to their work, and the wrong comment can ruffle feathers. I'll do my best to moderate and maintain diplomacy, but the general rule is: do unto others as you would have them do unto you. Don't be unnecessarily cruel, don't be spiteful, and don't be competitive. This is a collaborative effort.

#### To become an author <a id="tip3"></a>

1. Fork this repo
2. Create a folder for yourself in Authors, preferably kebab-case. See those already in there for inspiration.
3. Every post goes into its own folder, prefixed with the ordinal number of that post, and continuing with kebab-case of the title. For example, if you're writing about "validators in ethereum" and it's your first post, the folder should be called `01-validators` or something of the sort.
4. Every post's folder should have the subfolder `xx_XX` corresponding to the locale the content is written in. For English posts this will be `en_US` or `en_UK`, depending on your preference.
5. The content should be in a file called `final.md` in [Markdown](https://guides.github.com/features/mastering-markdown/) format.

In short, it should look like this:

![](https://imgur.com/vZNBua8.png)

#### To become a translator <a id="tip4"></a>

1. Fork this repo
2. Create a new locale folder under an existing post's parent folder \(i.e. `01-validators/es_ES/`\) and also put the translated content into a file named `final.md`
3. Submit a PR with the translation

#### About images <a id="tip5"></a>

To include images in your posts:

* put them into an images folder outside of all locales. So into `01-validators/images` in our example
* make sure they are optimized. Use ImageOptimize or Compressor.io and similar services and tools, they're great
* include them in posts as relative path to the markdown file. They will be uploaded to a dedicated CDN on publication

#### To become a reviewer <a id="tip6"></a>

1. Just chime in with comments.

That's it.

Okay, you can do a bit more if you want to.

* to contribute a fix to an already published post, send a PR with the fix
* to contribute a fix to a post that's in draft and being discussed \(i.e. not merged\), comment on that PR or even do a PR on that PR
* to discuss in general, check out the open issues and PRs and let your voice be heard in the comments

Note that fixes include everything from grammar and phrasing \(less important\) to content and breaking down explanations \(uber important\).

Other than that, you can also help by doing the following:

* suggest and discuss article topics under issues
* recruit more writers / developers to chime in
* help with grammar / phrasing if that's your forte
* donate your open source code and knowledge if you're not the writer type, and have someone else translate it to _humanese_ for you \(feel free to ping me - @swader - in an issue and I'll chime in asap!\)

### What's in it for me? <a id="tip7"></a>

* you help the community and spread the good word of Ethereum
* you train your writing skills and build a portfolio
* you get kudos when we implement some kind of Kudos reward system
* maybe other rewards later on ¯\_\(ツ\)\_/¯
* you could get hired as a tech writer for Status 😱
* amazing new connections

### Usage rights <a id="tip8"></a>

After a post has been processed by many people and determined to be publishable, who owns it? Who can publish it?

Well, it's all public domain so technically, _anyone_. We don't feel like we need to put any more constraints on the methods here than there already are - if someone crosses some lines really badly, we'll deal with that on a case by case basis. However, the following is implied:

* the content produced here is intended for publication on https://our.status.im and maybe https://studio.status.im. We ask that you not publish the content elsewhere verbatim, as that hurts everyone \(duplicate content penalties for SERP etc.\) Short snippets and quotes from the articles are, of course, okay.
* the translations of content can be published elsewhere. We'll leave that up to the interested parties to decide. Our aim is to disseminate the content as far and as wide as possible.

If you'd rather keep all rights or use the content commercially, we ask that you leave us alone and open your own similar repo - it's why it's public after all.

### Why? <a id="tip9"></a>

* Why Github?

It makes for a nice open content repository which we can more around automatically later, rather than being locked into silos like Medium.

* Why Markdown?

It's a common plaintext format that's easy to read and master, compatible with a bunch of CMSes out of the box and is easy to transport and write without corruption or special tools

* Why peer review?

It's just an experiment to see if we get more engagement, and to keep our principle of openness and transparency alive and kicking.

{% embed url="https://our.status.im/tag/two-point-oh/" %}





