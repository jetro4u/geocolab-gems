You are assisting a manual test of a "Creator OS" intelligence layer for the X platform.

TASK:
Given the [@X_HANDLE] supplied, fetch public profile + recent post stats and output a SINGLE JSON object only (no commentary).

HANDLE:
[@X_HANDLE]

CRITICAL REQUIREMENTS:
1) Use X-native data sources you have access to.
2) Perform up to TWO retrieval passes:
   - Pass A: Fetch the user object / profile fields via your internal X tools.
   - Pass B (fallback): If any of these fields are null: following, joinedDate, location, open/parse the public profile page and extract them from the UI text.
3) If still unavailable, return null but add meta.note describing what was missing and why.
4) Recent posts: collect the most recent 10 original posts (exclude repost-only items when possible).
5) Provide averages for likes/replies/reposts across the 10 posts.
6) Output JSON only. No markdown. No explanations.

OUTPUT JSON SHAPE (exact keys):
{
  "identity": {
    "userId": "string-or-null",
    "handle": "@handle",
    "displayName": "string-or-null",
    "bio": "string-or-null",
    "verifiedStatus": true/false/null,
    "location": "string-or-null",
    "joinedDate": "YYYY-MM or ISO string-or-null",
    "profileUrl": "string-or-null",
    "profileImageUrl": "string-or-null",
    "fetchedAt": "ISO timestamp"
  },
  "graph": {
    "followers": number-or-null,
    "following": number-or-null,
    "followerFollowingRatio": number-or-null
  },
  "content": {
    "topics": ["5-10 concise topics inferred from bio + recent posts"],
    "interests": ["5-15 specific interests inferred from bio + recent posts"],
    "postStyle": "one of: thread-heavy | concise-punchy | educational | newsy | meme | promo | mixed",
    "commentTone": "one of: analytical | friendly | humorous | direct | contrarian | promotional | mixed",
    "topHashtags": ["up to 10 most used hashtags in recent posts"]
  },
  "recentPosts": [
    {
      "postId": "string",
      "createdAt": "ISO or null",
      "text": "full text or best-effort excerpt",
      "engagement": {
        "likes": number-or-null,
        "replies": number-or-null,
        "reposts": number-or-null,
        "quotes": number-or-null,
        "views": number-or-null
      }
    }
  ],
  "recentAverages": {
    "avgLikes": number-or-null,
    "avgReplies": number-or-null,
    "avgReposts": number-or-null
  },
  "meta": {
    "note": "string-or-null"
  }
}