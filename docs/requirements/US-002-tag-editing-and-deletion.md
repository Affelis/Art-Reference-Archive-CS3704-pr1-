# User Stories: Art Reference Archive — Tag Editing and Deletion

## US-002 — Add and remove tags on one picture

**Story:** As the archive owner, I want to add and remove tags on a single existing picture, so that I can correct or extend the tags of a picture — including pictures imported from a ZIP — without deleting and re-uploading it.

**Acceptance Criteria**

1. Given a picture is shown in the gallery, when the user opens that picture's tag editor, then the editor shows the picture's current tags and provides controls to add tags and remove individual tags.
2. Given a picture displayed in the gallery that has the tags "nature" and "tree", when the user adds the tag "Forest" and confirms the edit, then the picture immediately displays the tags "nature", "tree", and "forest".
3. Given the tag "forest" was just added to a picture, when the application is restarted and the gallery is opened, then the picture still displays "forest" among its tags.
4. Given the user enters the tag "  Forest  " for a picture, when the edit is confirmed, then the picture's tag list contains "forest" and contains no tag with surrounding whitespace or uppercase letters.
5. Given a picture already has the tag "forest", when the user adds "Forest" or " forest " to that same picture, then the picture still shows exactly one "forest" tag and a message indicates the tag is already present.
6. Given the user enters an empty value or only whitespace as a tag, when the edit is confirmed, then the picture's tags are unchanged and a message indicates a tag cannot be empty.
7. Given the user enters "sky, water" as tags for one picture, when the edit is confirmed, then both "sky" and "water" are added to that picture.
8. Given two pictures both have the tag "sky", when the user removes "sky" from one of them and confirms, then that picture no longer shows "sky", the other picture still shows "sky", and searching by "sky" returns the other picture only.
9. Given a picture whose only tag is "sky", when the user removes "sky" and confirms, then the picture is saved with zero tags, remains present in the gallery, and displays "None" for its tags.
10. Given a picture was just edited to add the tag "forest", when the user filters the gallery, the random viewer, or the slideshow by "forest" without restarting the application, then that picture is eligible to be returned.
11. Given a picture's tag "forest" was just removed, when the user filters the gallery, the random viewer, or the slideshow by "forest" without restarting the application, then that picture is not returned.
12. Given the user cancels or abandons a tag edit before confirming it, when the user reloads the gallery, then the picture's tags are exactly as they were before the cancelled edit.

**Priority:** Must-have (MoSCoW)

**Related requirements:** No `REQ-###` or `UC-###` is assigned to this capability yet; this story is the origin of those IDs. Related stories: US-001 — ZIP-imported pictures arrive untagged, so this story is how they become searchable.

**Assumptions / dependencies:**

- Depends on `data.json` records continuing to hold tags per picture as a list of strings, and on the existing normalization rules (trim, lowercase, drop empty, no per-picture duplicates) being applied to edits as they are at upload time.
- Depends on the existing AND-semantics filtering; editing tags must not change which tag lists a filter can match.
- Confirmed scope: per-picture tag editing is available from the gallery and uses an explicit Save/Confirm action; the random viewer and slideshow do not need their own edit controls.
- Confirmed scope: changes are persisted when the user confirms the edit, not on each keystroke, so cancelling before confirmation leaves the stored tags untouched.
- Confirmed scope: a tag edit or a global rename cleans duplicate tags only on the pictures it actually changes; pictures it does not touch keep their existing records.
- The application is single-user and unauthenticated, so there are no permission checks and no loss-of-update concerns from concurrent editors.
- **Edge cases considered:** adding a case/whitespace variant of an existing tag (AC 5); empty or whitespace-only tag (AC 6); multiple comma-separated tags in one edit (AC 7); removing the last tag so the picture becomes untagged and displays "None" (AC 9); duplicate tags already present in a stored record are collapsed when that picture is next edited; a picture deleted in another view before the edit is confirmed is rejected with a message and the gallery refreshes; removing a tag that the current filter uses (AC 11).
