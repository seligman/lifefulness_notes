# Did the hackers just write a script?

*October 14, 2026*

> how do you think would the hackers have gone about identifying dormant podcasts like Sanderson's to target? Like, did they just write a script, or something? Is that just an easy thing to do?

Short answer, yes, finding quiet podcasts is really easy, and you don't even need a script. I doubt that's how they found Sanderson's show though, getting into his account was the hard part. My hunch is someone got in first, and the show being quiet just meant nobody noticed for a while. I looked for other shows hijacked like this and didn't find a single one.

(I'm calling them hackers to be kind here. I'm told Acast's support team identified a different email address as the one that took over his account, so I think that's fair, but we still don't know how they got in.)

## What happened, briefly

- October 14, 2021: the last real episode of *Lifefulness: Live Life Fully* (#66). The dates in its feed, and on the show's website, made it obvious it had gone quiet.
- May 18, 2026: a complete copy of the archive showed up on Spreaker (that's when Podcast Index first spotted it). Four days later, new episodes started appearing there, picking up the numbering at #67.
- June 26, 2026: the copy moved to RSS.com, and the Spreaker version was eventually set to forward there. Around the end of June it was renamed "Life Full On." The first new episodes were rewritten versions of *Therapy in a Nutshell* episodes, and later ones were Christian teaching.
- Somewhere along the way, the show's Apple Podcasts and Spotify listings started pointing at the copy.
- By early October: Acast had given Sanderson his account back, but Apple and Spotify still pointed at the copy (both are in his screenshots). I'm also told RSS.com handed back the copy and the money it had earned.
- Today: the RSS.com copy forwards to his original Acast feed, and Apple and Spotify are back on his original show. The old Spreaker copy has stopped forwarding and is up on its own again, with his archive and two of the hackers' episodes under his original title. Someone should get that taken down.

## Finding quiet shows

Like I said in the September 30 write-up, a show's feed is just a web address listing its episodes, and its Apple and Spotify listings (name, followers and ratings) point at that feed. Episodes come with dates, so a program can tell when a show last published without listening to it, nothing fancy. What it can't tell you is whether anyone still cares. (I'd know. I have a dormant podcast feed myself. It's not abandoned. It exists, it's just not my best work, which is why you're not getting a link.)

You don't even have to collect the feeds yourself. [Podcast Index](https://podcastindex.org/datasets) lets anyone download its whole directory: about 4.7 million shows in a 1.8 GB file, refreshed weekly, with the date of each show's newest episode (but not the contact email from each feed), and you don't need an account.

I used that file for my search in September, and today I timed it from scratch.

- Downloading it took under a minute here, so a minute or two on a typical home connection. Unpacking it took about 25 seconds.
- One query listed every show whose newest episode was two to five years old on May 18: about 1.3 million shows, in a couple of seconds. (Two to five years was my own rough guess at what a hacker might call "quiet." We don't know if they used any rule at all.)
- Keeping only shows with a working feed, an Apple Podcasts listing and at least 20 episodes brought it down to about 266,000.

(I don't have May's copy of the file, so I rebuilt those numbers from this month's. That barely moves them.)

Sanderson's show is on that list, but it doesn't stand out: by Podcast Index's rough popularity score, about 14,000 shows on the list rank above it. Being quiet isn't unusual, either. More than 70% of the shows in Podcast Index haven't had a new episode in two years.

Here's more or less the whole "script":

```sql
SELECT title, url FROM podcasts
WHERE newestItemPubdate BETWEEN 1621296000 AND 1715990400  -- last episode mid-May 2021 to mid-May 2024
  AND lastHttpStatus = 200                                  -- the feed still works
  AND typeof(itunesId) = 'integer' AND itunesId > 0         -- it has an Apple Podcasts listing
  AND episodeCount >= 20;                                   -- at least 20 episodes
```

(The big numbers are dates, in seconds since 1970.)

You might not even need that much:

- The Podcast Index file opens in a free point-and-click database program, and James Cridland of Podnews has published copy-and-paste queries for it (his are for industry stats, like counting the shows that stopped after one episode).
- If you'd rather pay, Listen Notes sells podcast data as spreadsheet files from $1, with each show's latest episode date and, when it has one, the publisher's email. Finding the quiet ones is just a filter.
- MillionPodcasts is a database for booking podcast guests. It has "latest episode date" and "has email" filters right on its web page, and starts at about $12 a month, billed yearly.
- Pay-per-result scrapers built for PR outreach, about $30 to $40 per 1,000 shows, read each feed's owner email and last episode date.

(These are all normal tools, and I've got no reason to think any of them were used here.)

## What a list like that would tell them

I fetched 1,200 random feeds from the same kind of list, built as of this month. Of the ones that loaded, about 88% list a contact email, and for about 40% it's a personal one like Gmail. Only about 8% carry a "please don't import me" flag.

A few of those addresses are a risk on their own. About 4% of the shows using an email address on their own domain have a domain that doesn't exist any more, most likely because it lapsed. Whoever registers it next gets that email, including any "prove you own this podcast" messages. That doesn't fit Sanderson's case: the archived copies of his feed from before the hijack (2021 and 2022) only list Acast's forwarding address. (There are no archived copies from 2023 to 2026.)

A list-maker can't see the real listener numbers, which are behind the owner's login. They get roughly what you or I can see: the episode list, the ratings (4.9 stars from 33 ratings for Sanderson's show, according to Podnews) and maybe a rough popularity score.

## Copying a show vs. taking it over

Copying a podcast is easy, and it happens a lot. Spreaker has an importer for moving your own show over, and all it needs is a show's public feed address. It copies the whole archive in a couple of minutes. In September I found hundreds of copies of other people's shows. Nearly all were copies of shows that were still running, and most looked like people keeping a copy for themselves or giving a new show something to start with.

In Sanderson's case his original Apple and Spotify listings went along with the copy, and that part is rare. Those listings came with hundreds of followers each, plus years of ratings, and moving them takes control of the show itself. There are only a few ways to do that: a redirect on the old feed (a setting in his Acast account that tells apps "this show lives over there now"), changing the feed address in his Apple or Spotify podcaster dashboard, "claiming" the show with a code that either goes into the feed or gets sent to the feed's email, or talking a support team into it. Except for the last one, all of those need a login.

And in the archived copies from before the hijack, Sanderson's feed listed Acast's forwarding address, which Acast says passes verification codes from Apple, Spotify and Google on to the email set in the show's settings. So whoever controlled the Acast account probably controlled where those codes went too, and that one account could have been enough for everything.

We don't know which route they used. When Sanderson took his screenshots in early October, the show was still in his own Apple and Spotify accounts, just pointed at the copy, so it doesn't look like anyone claimed it away from him. A redirect set from his Acast account would have moved both in one go, so that's my best guess. I can't check it, because the Wayback Machine and other web archives have no copies of his Acast feed from 2026. (An AI assistant I asked back in August said his Acast feed was redirecting to Spreaker then, but it didn't save a copy.)

Apple's help says a redirect "updates Apple Podcasts with the new feed URL," and you only have to keep it up for four weeks. After that the old address doesn't matter, and Spotify acted the same way here. That's why getting the Acast account back didn't fix them. The fix probably worked the same way in reverse: the RSS.com copy now redirects to Sanderson's original feed, and the listings followed it back.

RSS.com checks that you control a show before importing it, by having you add the word "RSSVERIFY" to its description at the current host. That word is still sitting in the Spreaker copy's description, so as far as I can tell the hackers passed the check with the copy they'd made themselves. From RSS.com's side, it would have looked like a normal move.

Feeds can carry a flag asking other hosts not to import them, but it couldn't have helped here. Acast doesn't add it (none of the roughly 9,800 Acast feeds I checked had it), and neither does Spotify's own hosting service. It's only a polite request anyway, and it does nothing against someone already logged into the account. (The hackers' RSS.com copy had it, because RSS.com turns it on by default.)

## So did they go looking for quiet shows?

Maybe they made a list of quiet shows (or just came across his), picked it, and then found a way in. Or maybe they got into an account first, somehow, and the podcast was what they found there.

I can't tell those apart, and either way someone had to get into his Acast account, which a list won't do for you. The usual ways in are a password reused from an old breach, a phishing email, a hacked mailbox used to reset the password, or talking a support team into it. A reused password is what getting in first can look like. In 2020 someone tried hundreds of millions of logins, probably leaked from other sites, against Spotify and got into an estimated 300,000 to 350,000 accounts, whichever ones happened to work. I don't know which, if any, of these happened here.

I lean toward them getting in first. For one thing, I couldn't find anyone else this happened to. In September I went through all 4.7 million shows in Podcast Index, fetched about 352,000 feeds, ran four different detectors built to catch exactly this pattern, and checked about 71,000 quiet shows' Apple listings directly. All four detectors found Sanderson's show, and none found another. If someone had a list of a quarter of a million targets and a reliable way in, I'd expect more than one victim.

I also couldn't find any reports of anything like it. Searching the news for podcast takeovers since 2018 turned up copycats re-uploading popular shows and spam podcasts made from scratch, but no quiet shows taken over like this. The closest I found was back in 2005, when someone pointed a podcast's directory listings at a site they controlled, then wanted money to put them back.

So it's possible they worked from a list, but I haven't found anything to back it up. I also didn't see any sign they were going after shows that had been quiet for some set stretch, like "two to five years." Shows come back after long breaks every month, and nearly all the ones I looked at closely were their owners picking things back up, renaming, moving hosts or reusing their own feed.

My search has gaps, I only got through about 500 shows on Spotify before it cut me off for a day and I called it quits there. I didn't cover other directories, very small shows' Apple listings, or anything deleted before late September. And failed attempts don't leave public traces.

## Why a quiet show is worth stealing

- It has hundreds of followers on Apple and on Spotify, and their apps grab whatever new episodes appear in the feed.
- The old episodes can earn money too. RSS.com's ad program puts ads into "both new and existing episodes" and pays out 60 to 90 days after they run, so my guess is a lot of what the hackers earned was still sitting there when RSS.com gave it back. Separately, Sanderson's Spotify stats show a big jump in plays of the old episodes after the takeover, with oddly similar numbers for each one, which made him wonder if they were bought. I can't tell, and his Apple numbers barely moved.
- Nobody's checking it every week, so they could expect a head start. They had it for about four months before Sanderson got his Acast account back, and Apple and Spotify stayed on the copy into October.

Nothing I've seen suggests this was about Sanderson personally.

## What I still don't know

- How the hackers got into the Acast account.
- How Apple and Spotify were moved to the copy.
- Whether they picked his show from a list, or found it after getting in.
- Why they went through Spreaker before RSS.com.
- Whether those extra plays were real people, and how much money the hackers made.

Acast can say how and when the other email address got onto the account (a login followed by an email change, a password reset, an invitation, or a support ticket), and Spreaker, RSS.com, Apple and Spotify can fill in the rest. Sanderson may be able to narrow it down himself from any emails Acast sent him in the spring, like password resets or notices that someone's access to the show changed.

## If you have a quiet show

If you've got a quiet show (and I do), here's what I'd do:

- Use a unique password and two-step login (a code from your phone as well as the password) on the email account behind your podcast, and on your host and Spotify if they offer it. Whoever gets into that mailbox can reset almost everything else.
- If your host hides your email address in the feed, leave that on. (On Acast it's the "Obfuscate Email" switch.)
- In Apple Podcasts Connect (Apple's dashboard for podcasters), turn on "Don't allow show to be claimed."
- If the email in your feed is on your own domain, keep the domain renewed.
- Every so often, check that your Apple and Spotify listings still point at your feed.

## Sources

*Links checked October 14, 2026.*

### Finding shows

- Podcast Index, [public datasets](https://podcastindex.org/datasets): the free weekly download. Most field definitions are in the [API docs](https://podcastindex-org.github.io/docs-api/), but I couldn't find the popularity score documented anywhere.
- James Cridland, [Data mining the Podcast Index](https://james.cridland.net/blog/2026/podcast-index-sql-data-mining/) (June 2026).
- Listen Notes, [podcast datasets](https://www.listennotes.com/podcast-datasets/), [data fields](https://www.listennotes.com/podcast-datasets/fields/) and its [PR guide](https://www.listennotes.help/article/104-podcast-pr-guide-how-to-find-podcasts-and-reach-out-to-be-a-guest) ("Starting at US $1").
- [MillionPodcasts](https://www.millionpodcasts.com/), whose filters include "Latest episode date" and "Has email".
- Two pay-per-result scrapers on the Apify marketplace, both built for PR outreach: [Podcast Finder & Host Email Extractor](https://apify.com/piposlab/podcast-leads-extractor) and [Podcast Email Scraper](https://apify.com/ritaya/podcast-email-scraper).

### Moving a listing

- Apple: [Change the RSS feed URL](https://podcasters.apple.com/support/837-change-the-rss-feed-url) and [Claim your show](https://podcasters.apple.com/support/5497-claim-your-show) (including the "Don't allow show to be claimed" setting).
- Spotify: [Updating an RSS feed link](https://support.spotify.com/us/creators/article/updating-an-rss-feed-link-or-hosting-provider/) and [Claiming your podcast](https://support.spotify.com/us/creators/article/claiming-your-podcast-on-spotify-for-creators/).
- Acast: [How to redirect your podcast](https://learn.acast.com/en/articles/5087325-how-to-redirect-your-podcast-cancel-your-subscription-or-delete-your-account) and [email masking](https://learn.acast.com/en/articles/3505483-how-to-find-and-unmask-your-show-s-email-address) (forwarded verification codes, and the "Obfuscate Email" switch).
- Spreaker: [RSS Feed Importer](https://help.spreaker.com/en/articles/3753095-how-to-import-your-podcast-with-the-rss-feed-importer).
- RSS.com: [Claim ownership of your podcast](https://help.rss.com/en/support/solutions/articles/44002406285-how-to-claim-ownership-of-your-podcast-hosted-outside-rss-com) (the RSSVERIFY step).
- The [podcast:locked](https://github.com/Podcastindex-org/podcast-namespace/blob/main/docs/tags/locked.md) tag.

### Money

- RSS.com: [PAID ads](https://help.rss.com/en/support/solutions/articles/44002610298-what-are-programmatic-ads-inserted-dynamically-paid-) and [how PAID payouts work](https://help.rss.com/en/support/solutions/articles/44002649174-how-paid-payouts-work).

### Earlier cases

- The Register, [Podcast hijacked by 'extortionist'](https://www.theregister.com/2005/12/02/podjacking/) (2005).
- Techdirt, [Dealing With Podcast Copycats (2020)](https://www.techdirt.com/2021/04/09/content-moderation-case-study-dealing-with-podcast-copycats-2020/).
- BleepingComputer, [Spotify abused to promote pirated software and game cheats](https://www.bleepingcomputer.com/news/security/spotify-abused-to-promote-pirated-software-and-game-cheats/) (2024).
- BleepingComputer, [Over 300K Spotify accounts hacked in credential stuffing attack](https://www.bleepingcomputer.com/news/security/over-300k-spotify-accounts-hacked-in-credential-stuffing-attack/) (2020).

### This case

- Sanderson's screenshots of his Acast, Apple and Spotify dashboards (early October): his Acast account reinstated, Apple Podcasts Connect still pointing at the copy on October 1 (and Spotify too), and the jump in plays of old episodes.
- Podnews, [the show's page](https://podnews.net/podcast/i61j2) (cached September 30, so it still shows the copy).
- The show's [website](https://www.lifefulness.io/podcast).
- My September 30 search, and today's download timing, feed sample and checks, are in my investigation notes.
