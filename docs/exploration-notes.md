# Exploration Notes: RealWorld (Conduit)

- **App URL:** https://demo.realworld.show/
- **Date:** 2026-10-12 to 2026-10-14
- **Tester:** Hemlal
- **Browser:** Microsoft Edge Version 155.0.4283.45 (Official build) (64-bit)

## 1. Features found

### 1. Sign up

- Entering username, email and password creates the account.
- The user is logged in and redirected to the Global Feed.
- The username appears in the top menu.

### 2. Login

- Signs in with **email** and password (username does not work).
- Success redirects to the Global Feed.
- The Sign in button is disabled when a field is empty.
- Wrong password and unknown email both show the same generic "credentials invalid" error (no user enumeration).

### 3. Create article

- The New Article form has title, description, body and tags.
- After publishing, the article opens at `/article/<title-slug>`.
- The article page shows author, date, tags, Edit/Delete buttons and a comment box.
- Empty title: Publish shows "title can't be blank" and no article is created. The other field values are kept.
- Empty body: Publish shows "body can't be blank" and no article is created. The other field values are kept.
- Duplicate title: a second article with the same title is created. The app makes the URL unique by adding a suffix (`/article/qa-test-article-01-1`), so the first article is not overwritten.

### 4. Edit article

- Edit Article opens the form with the existing values.
- Changing the title and publishing updates the article. The body and author are unchanged.
- The URL slug changes with the new title (`/article/qa-test-article-01-edited`).
- Edit with an empty title: no validation error is shown. The app redirects to `/article/` (blank page). Afterwards the article appears in the profile list without a title.

### 5. Delete article

- Delete Article on an own article removes it and redirects to the Home page (Global Feed).
- The deleted article no longer appears in the Global Feed or in the profile's My Posts list.
- No confirmation dialog is shown. The article is deleted immediately after clicking Delete Article.

### 6. Comment

- A comment box ("Write a comment...") with a Post Comment button appears below the article.
- Posting a comment adds it below the box with the author, date and a delete (trash) icon. The comment box is cleared after posting.
- Empty comment: Post Comment shows "body can't be blank" and no comment is created. The button stays enabled (error appears after clicking, same as New Article).
- Delete comment: clicking the trash icon removes the comment immediately, without a confirmation dialog.

### 7. Favorite

- Clicking the heart on an article favorites it: the count increases by 1 and the heart is filled. Clicking again removes the favorite and the count decreases by 1.
- Works on other users' articles (count 2 to 3 on "How to Learn JavaScript Efficiently") and on own articles.
- Favorited Posts tab on the profile (`/profile/<username>/favorites`) lists the favorited article ("How to Learn JavaScript Efficiently") with the updated count.

### 8. Follow user

- Your Feed (`/?feed=following`) shows "Your feed is empty. Follow some users to see their articles here, or check out the Global Feed!" when the user follows nobody.
- Opening another user's profile (`/profile/johndoe`) shows their bio and articles. Clicking Follow changes the button to "Unfollow johndoe".
- After following johndoe, Your Feed lists johndoe's article.
- Clicking "Unfollow johndoe" changes the button back to "Follow johndoe". After unfollowing, Your Feed shows the empty-feed message again.

### 9. Tag filter

- Clicking a tag in Popular Tags (e.g. `javascript`) opens `/tag/javascript` with a new "# javascript" tab.
- Only articles that have the selected tag are listed: `javascript` shows 2 articles, `python` shows 1 article ("Introduction to Machine Learning for Developers").
- Empty tag result (a tag with no articles): not tested.

### 10. Profile settings

- The Settings page (`/settings`) has fields for profile picture URL, username, bio, email and new password, plus an Update Settings button and a logout button.
- Username and email are pre-filled with the current values. The other fields are empty.
- Updating the bio redirects to the profile page, where the new bio is shown under the username.
- Changing the username redirects to the new profile URL (`/profile/qa_hemlal02`). The new username appears in the top menu and as the author of existing articles. The bio is kept.
- Changing the password: the old password is rejected ("credentials invalid") and the new password signs in successfully.
- Changing the email: the old email is rejected ("credentials invalid") and the new email signs in successfully.

## 2. Questions (unclear behaviour)

- Login disables the Sign in button for empty fields, but New Article and Comment keep their buttons enabled and show an error after clicking. Is this difference intended?
- After editing a title, the old URL stops working. Should the app redirect, or at least show a "not found" message?
- Delete Article and Delete Comment both remove the item immediately without a confirmation dialog. Is this intended? An accidental click cannot be undone.
- Is it intended that an article can be favorited by its own author?

## 3. Suspicious things (possible bugs)

- Opening any non-existent article URL (e.g. `/article/this-does-not-exist-999`, or the old slug `/article/qa-test-article-01-1` after a title edit) shows a blank page with only the header. No "Article not found" message is shown. Severity: Low.
- Editing an article and clearing the title saves it without any error. The app redirects to `/article/` (blank page). The article then appears in the profile list and Global Feed without a title, and clicking it opens a blank page, so its Edit and Delete buttons cannot be reached from the UI. Create article rejects an empty title, Edit does not. Severity: High.
- Note: both findings were observed on 2026-10-13. They have not yet been re-checked on a later date.

## 4. Environment notes

- The demo site shows a banner: "This demo is connected to a demo backend that enforces session isolation."
- On 2026-10-14 at about 12:00, after logging in again, the Global Feed showed only the 4 seed articles and the favorite counts were at their seed values. The articles created on 2026-10-13 were not visible.
- On 2026-10-14 at about 15:26, the same account showed the 2026-10-13 articles and the favorite again, together with a new article created that day.
- Logging out and logging in again (checked on 2026-10-15) does not remove the data: the article "Persistence Check" was still present.
- The cause of the temporary disappearance on 2026-10-14 is not confirmed. The demo data may be temporarily inconsistent.
- Consequence: results on this demo may not be repeatable. Tests should create their own data, and a local backend gives a more reliable environment.
