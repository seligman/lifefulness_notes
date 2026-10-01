# Was what happened to the Lifefulness podcast part of a bigger campaign?

As far as I can tell, no. What happened to Lifefulness looks like a one-off. I checked hundreds of thousands of podcasts, and Lifefulness was the only show that matched the whole pattern.

Along the way I learned that copying other people's podcasts is surprisingly common. But the copies are almost always of shows that are still running, and apart from Lifefulness, none of them ended up with the original show's listing pointing at the copy.

## Some background

A podcast is really just a web address (the feed) that lists the episodes. Apps like Apple Podcasts and Spotify keep a listing for each show (its name, reviews and subscribers), and that listing points at the show's feed. If the feed a listing points to changes, everyone subscribed to the show starts getting whatever the new feed publishes.

*Lifefulness: Live Life Fully* was a podcast by Sanderson Jones. It stopped in October 2021, after 66 numbered episodes. In May 2026, after four and a half years of silence, new episodes started appearing under a new name, "Life Full On."

What had happened:

- A complete copy of the old show's episode archive had been set up on a different podcast host.
- The show's Apple Podcasts listing now points at that copy, so existing subscribers see the new episodes.
- The new episodes continued the old numbering (#67, #68, #69 and so on).
- The first three were reworded versions of episodes from a completely unrelated show, *Therapy in a Nutshell*.
- Later episodes switched to Christian teaching.

The original feed still exists, untouched, and nothing on it says the show moved. I don't know who changed the listing.

## What I did

If someone was doing this on purpose, I'd expect to find other shows with the same pattern: years of silence, a copied archive, the old listing quietly pointing at the copy, and recycled content from someone else. So I went looking.

1. Got a list of nearly every podcast from Podcast Index, an open podcast directory that publishes its whole database: about 4.7 million shows. Older copies from 2020 and 2021 via archive.org told me what shows *used* to be called and who made them.
2. Downloaded the actual episode lists of about 352,000 shows. That's every show that could possibly have gone quiet for two or more years and then come back in 2025 or 2026. About 24,000 of them did.
3. Built four different takeover detectors, each looking for the Lifefulness pattern a different way:
   - shows whose old archive suddenly appeared in a brand-new feed
   - feeds that share episodes with another feed (copies)
   - shows whose episode list has years of silence followed by new episodes
   - old, quiet shows whose Apple listing now points somewhere new, under a new name (I checked about 71,000 quiet shows' listings directly with Apple)
4. Reviewed the ~1,060 most suspicious shows one by one. Wrote some scripts to look at each show and who made each show before and after. They looked for signs that a change was legitimate, and searched the web for where the new content came from, at least until the search API allowance ran out. Anything still suspicious got dumped out for me to manually review to prove it innocent.
5. Compared the audio. I used voice-matching software for the voices and automatic transcripts for what was said. I did both on Lifefulness itself and against *Therapy in a Nutshell*, the show its material came from.

## What I found

### Lifefulness itself

Some more detail, though how the listing was moved is still unknown:

- The copy first showed up, on a hosting service called Spreaker, four days before the first new episode.
- In late June, the whole copy moved to a second host, RSS.com, in a single upload that took three and a half minutes. That copy was the old archive (68 items) plus the first two new episodes.
- Each of the first three "new" episodes is a reworded version of a specific *Therapy in a Nutshell* episode. They keep that show's particular examples and stories, but the wording is rewritten and read by a different narrator.
- The narrator is clearly not *Therapy in a Nutshell*'s host, Emma McAdam. I couldn't tell whether the narrator is a real person or a computer-generated voice.

### No second case

All four detectors found Lifefulness again, and no other show matched the pattern. Almost all of the shows that looked suspicious on paper had an ordinary explanation:

- the same person renaming their own show, or picking it back up after a break
- a company or church reusing its own feed
- a show moving to a new hosting company

A few I just couldn't figure out (dead websites, accounts whose ownership history isn't public, content farms), and a few others were suspicious copies of a different kind, more on those below.

There was no clustering by restart date, hosting company, names or voices that would suggest one group behind several shows. The only big cluster was one audiobook publisher restarting about 300 of its own feeds in the same July week, which is not a takeover, just businesses doing business things.

Of the ~71,000 quiet shows I checked on Apple, 425 now have listings pointing to a different, active show under a new name, and I looked over all of them. Apart from Lifefulness, they were mostly the same people rebranding or resuming, companies folding shows together, or mix-ups. A handful stayed unclear, I think just people trying new things out and/or cross-brand promotions, but none looked like Lifefulness.

### Copied podcasts

I found hundreds of feeds that had copied most or all of another show's archive into a new feed under a different name. Some of the copied shows were *The Daily*, *Dateline NBC*, *Crime Junkie* and The Economist's podcasts. In nearly all of these, the original show was still running. No doubt this is just a cross branding sort of thing.

A smaller number of copies were of long-dormant shows, like Lifefulness. Apart from Lifefulness, whenever a listing followed a copy, it was the same publisher moving its own show.

A few copies did look deliberately shady:

- An old Australian audio-art podcast called *The Market Research* was copied and used to post an ad (about phone-service providers) for a US marketing firm. It seems to have been picked purely for the words in its name, if I had to guess, money changed hands here.
- A popular Indian wellness show's archive was copied and topped up with short clips that look like they were taken from a video. No clue about this one.
- Two accounts were re-posting a popular true-crime show, *Casefile*, under names that have nothing to do with it. One of them re-posts every episode. Might be something here, but again, no idea.

### Recycled addresses and listings

In some cases an old show's address or listing now belongs to a different publisher. That can happen when someone gives up a username or website and somebody else grabs it later, or when whoever controls the listing points it somewhere new. Most of the ones I found look innocent, and none looked like Lifefulness, but it's one more way a quiet show's listing could end up somewhere unexpected.

## Gaps

- Only Apple or the hosting companies involved can say how the Lifefulness listing was moved.
- I could only check Apple Podcasts listings, so a takeover that only happened on Spotify would have slipped past me. Note: I've since gotten Spotify API access, and I'm working on this side.
- I didn't check the listing of every tiny show, and shows deleted before September 2026 aren't in the data.

## My take

I don't think this was a campaign looking at podcasts to find a mark. I checked hundreds of thousands of shows and found no other case. Copying the old episodes to a new host didn't take any special access, anyone can import a public feed. Pointing the show's existing Apple Podcasts and Spotify listings at the copy did. That could have been done by someone who got into the creator's Apple or Spotify login, or the Gmail account behind the show. One plausible way in would be a password reused from an old breach. Someone could have been trying to sign into accounts till they got hits, and found one that was dormant.
