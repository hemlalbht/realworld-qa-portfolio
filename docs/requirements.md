# Requirements: RealWorld (Conduit)

- **Version:** 0.2
- **Status:** Draft for review
- **Date:** 2026-10-14
- **Basis:** Derived from exploratory testing of https://demo.realworld.show/ (no original specification was provided).
- **Note:** Requirements marked "(inferred)" describe expected behaviour that the application does not currently meet, or that was not observed directly.

## Modules

| Code | Module                    | Requirements      |
| ---- | ------------------------- | ----------------- |
| AUTH | Authentication            | REQ-AUTH-01 to 03 |
| ART  | Articles                  | REQ-ART-01 to 07  |
| COM  | Comments                  | REQ-COM-01 to 03  |
| SOC  | Social (favorite, follow) | REQ-SOC-01 to 04  |
| DIS  | Discovery (feeds, tags)   | REQ-DIS-01 to 02  |
| PRO  | Profile                   | REQ-PRO-01 to 02  |

---

## AUTH: Authentication

### REQ-AUTH-01: Sign up

**Statement:** The system shall allow a new user to create an account with a username, email and password.

**Acceptance criteria:**

- Valid username, email and password creates the account.
- After sign up, the user is logged in and redirected to the Global Feed.
- The username appears in the top menu.

**Source:** Exploration notes, Feature 1

### REQ-AUTH-02: Login

**Statement:** The system shall allow a registered user to sign in with email and password.

**Acceptance criteria:**

- Valid email and password signs the user in and redirects to the Global Feed.
- Signing in with a username instead of an email is rejected.
- Invalid credentials show the error "credentials invalid".
- The error message is the same for a wrong password and an unknown email.
- The Sign in button is disabled while a field is empty.

**Source:** Exploration notes, Feature 2

### REQ-AUTH-03: Logout

**Statement:** The system shall allow a logged-in user to log out from the Settings page.

**Acceptance criteria:**

- "Or click here to logout." ends the session and opens the Home page.
- After logout, the top menu shows Home, Sign in and Sign up instead of the username.
- After logout, only the Global Feed tab is shown (Your Feed is hidden).

**Source:** Exploration notes, Feature 10

---

## ART: Articles

### REQ-ART-01: Create article

**Statement:** The system shall allow a logged-in user to publish an article with a title, description, body and optional tags.

**Acceptance criteria:**

- Valid title, description and body publishes the article.
- The article opens at `/article/<title-slug>`.
- The article page shows the author, date, body, tags, Edit/Delete buttons and a comment box.
- The article appears in the Global Feed and in the author's profile.

**Source:** Exploration notes, Feature 3

### REQ-ART-02: Create article validation

**Statement:** The system shall reject an article with an empty title or an empty body.

**Acceptance criteria:**

- Empty title shows "title can't be blank" and no article is created.
- Empty body shows "body can't be blank" and no article is created.
- The values entered in the other fields are kept.

**Source:** Exploration notes, Feature 3

### REQ-ART-03: Unique article URL

**Statement:** The system shall create a unique URL for each article, including articles with the same title.

**Acceptance criteria:**

- Publishing a second article with an existing title creates a new article.
- The new article gets a different URL (for example `/article/qa-test-article-01-1`).
- The first article is not overwritten.

**Source:** Exploration notes, Feature 3

### REQ-ART-04: Edit article

**Statement:** The system shall allow the author to edit their own article.

**Acceptance criteria:**

- Edit Article opens the form with the existing values.
- Changing the title and publishing updates the article.
- The URL changes to match the new title.
- The body and author are unchanged.

**Source:** Exploration notes, Feature 4

### REQ-ART-05: Edit article validation (inferred)

**Statement:** The system shall reject an edit that leaves the title empty, in the same way as article creation.

**Acceptance criteria:**

- Empty title shows "title can't be blank" and the article is not changed.
- An article can never be saved without a title.

**Source:** Exploration notes, Feature 4 and Suspicious things (observed behaviour does not meet this requirement)

### REQ-ART-06: Delete article

**Statement:** The system shall allow the author to delete their own article.

**Acceptance criteria:**

- Delete Article removes the article and redirects to the Home page.
- The deleted article no longer appears in the Global Feed or in the profile's My Posts list.
- No confirmation dialog is currently shown (see Open questions).

**Source:** Exploration notes, Feature 5

### REQ-ART-07: Article not found (inferred)

**Statement:** The system shall show a clear "not found" message when an article URL does not exist.

**Acceptance criteria:**

- A non-existent article URL shows a "not found" message.
- A previous URL of an edited article shows a "not found" message or redirects to the new URL.
- The page is never blank apart from the header.

**Source:** Exploration notes, Suspicious things (observed behaviour does not meet this requirement)

---

## COM: Comments

### REQ-COM-01: Post comment

**Statement:** The system shall allow a logged-in user to post a comment on an article.

**Acceptance criteria:**

- A valid comment appears below the comment box with the author, date and a delete icon.
- The comment box is cleared after posting.

**Source:** Exploration notes, Feature 6

### REQ-COM-02: Comment validation

**Statement:** The system shall reject an empty comment.

**Acceptance criteria:**

- Empty comment shows "body can't be blank" and no comment is created.

**Source:** Exploration notes, Feature 6

### REQ-COM-03: Delete comment

**Statement:** The system shall allow the comment author to delete their comment.

**Acceptance criteria:**

- The trash icon removes the comment from the article.
- No confirmation dialog is currently shown (see Open questions).

**Source:** Exploration notes, Feature 6

---

## SOC: Social

### REQ-SOC-01: Favorite and unfavorite article

**Statement:** The system shall allow a logged-in user to favorite and unfavorite an article.

**Acceptance criteria:**

- Clicking the heart increases the count by 1 and fills the heart.
- Clicking it again decreases the count by 1 and removes the fill.
- Works on other users' articles and on own articles.

**Source:** Exploration notes, Feature 7

### REQ-SOC-02: Favorited Posts list

**Statement:** The system shall list a user's favorited articles on their profile.

**Acceptance criteria:**

- The Favorited Posts tab (`/profile/<username>/favorites`) lists the favorited articles with the current count.

**Source:** Exploration notes, Feature 7

### REQ-SOC-03: Follow and unfollow user

**Statement:** The system shall allow a logged-in user to follow and unfollow another user.

**Acceptance criteria:**

- The Follow button on another user's profile changes to "Unfollow <username>" after following.
- Unfollow changes the button back to "Follow <username>".

**Source:** Exploration notes, Feature 8

### REQ-SOC-04: Your Feed

**Statement:** The system shall show the articles of followed users in Your Feed.

**Acceptance criteria:**

- After following a user, Your Feed (`/?feed=following`) lists that user's articles.
- After unfollowing, those articles are removed from Your Feed.
- When the user follows nobody, the message "Your feed is empty. Follow some users to see their articles here, or check out the Global Feed!" is shown.

**Source:** Exploration notes, Feature 8

---

## DIS: Discovery

### REQ-DIS-01: Global Feed

**Statement:** The system shall show all articles in the Global Feed with the popular tags list.

**Acceptance criteria:**

- Each entry shows the author, date, title, description, tags and favorite count.
- The Popular Tags list is shown on the right.

**Source:** Exploration notes, Features 1 and 2 (observed on the home page)

### REQ-DIS-02: Tag filter

**Statement:** The system shall filter the article list by a selected tag.

**Acceptance criteria:**

- Clicking a tag opens `/tag/<tag>` with a "# <tag>" tab.
- Only articles that have the selected tag are listed.

**Source:** Exploration notes, Feature 9

---

## PRO: Profile

### REQ-PRO-01: View profile

**Statement:** The system shall show a user's profile with their bio and articles.

**Acceptance criteria:**

- `/profile/<username>` shows the username, bio, My Posts and Favorited Posts tabs.
- On the own profile, an Edit Profile Settings button is shown.

**Source:** Exploration notes, Features 7, 8 and 10

### REQ-PRO-02: Update settings

**Statement:** The system shall allow a logged-in user to update their profile picture, username, bio, email and password.

**Acceptance criteria:**

- Update Settings with a new bio shows it on the profile page.
- A new username opens the new profile URL and updates the author name on existing articles.
- A new email replaces the old one: the old email is rejected at login, the new one signs in.
- A new password replaces the old one: the old password is rejected, the new one signs in.

**Source:** Exploration notes, Feature 10

---

## Open questions (to clarify with the product owner)

1. 1. Should empty-field validation be consistent? Sign in is disabled for empty fields, but New Article and Comment stay enabled and show an error after clicking.
2. Should Delete Article and Delete Comment ask for confirmation?
3. Is it intended that an author can favorite their own article?
4. After an article title is edited, should the old URL redirect to the new one or show a "not found" message?
