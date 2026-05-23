# Hostinger Video Embed Fix
TLDR: Use on customizable websites such as Hostinger and Wordpress to avoid broken "video URL" errors. It will even round your corners. Visitors now see a preview image (not a blank black box) until they click play.

## OVERVIEW
This code solves a common issue when embedding a Google Drive-hosted video inside a website builder like Hostinger: the video may display correctly on desktop, but look misaligned on mobile, lose its rounded-corner crop, or refuse to sit centered inside the visible frame. It also fixes the problem where the embed looks empty or black before anyone clicks—by showing a preview image first, then loading the real player only after a click.

The solution uses a wrapper element to control the visible crop area and positions the embedded iframe so the video stays centered and visually consistent across screen sizes. A preview image (called a "poster") sits on top until the visitor is ready to watch.

This embed is designed to display a Google Drive-hosted video in a responsive, cropped frame with rounded corners. The wrapper controls the size and positioning of the video so it stays centered on desktop and mobile, but the interactive playback controls still depend on Google Drive's embedded player, which can behave inconsistently on mobile browsers.

## WHAT THIS CODE DOES
Shows a preview image and play button as soon as the page loads (so the box is never blank).

Loads the Google Drive player only after someone clicks (this is called "lazy loading" and it avoids the empty black frame).

Creates a fixed aspect-ratio video box for a clean desktop layout.

Uses overflow: hidden and border-radius to crop the video with curved edges.

Centers the iframe inside the box with CSS positioning and transforms.

Nudges the video slightly on mobile so the visible part stays better aligned.

Keeps the embed responsive so it scales down naturally on smaller screens.

## BEFORE YOU START (BEGINNER NOTES)
You do not need to install anything. You copy one file from this repo, change two placeholders in the code (all are labled Steps 1 to 3), and paste it into Hostinger.

A "file ID" is the long code in the middle of your Google Drive link. Example link:

https://drive.google.com/file/d/1aBcDeFgHiJkLmNoPqRsTuVwXyZ/preview

The file ID is everything between /d/ and /preview:

1aBcDeFgHiJkLmNoPqRsTuVwXyZ

In the code you will replace YOUR_FILE_ID with that exact string (there are 2 placeholders in the file).

## WALKTHROUGH
Open Google Drive, find your video, and remove all sharing restrictions (ie Anyone on the internet with the link can view).

Open the file named <div class="video-shell">.html in this repository (or copy all of its contents).

Find YOUR_FILE_ID in the file. There are two spots. Replace both with your real file ID from step 1. Do not delete the rest of the link—only swap the placeholder text.

Optional: If the automatic preview image looks wrong, see "CUSTOM PREVIEW IMAGE" below.

On Hostinger, add a new code <> element (Custom HTML / Embed code).

Paste the entire file—HTML, style, and script together in one block.

Save and preview your page on desktop and on your phone. You should see the preview image first; after you click, the video player should appear inside the rounded frame.

## IF THE PREVIEW IMAGE DOES NOT SHOW
Make sure sharing is set to Anyone with the link can view.

Double-check that you copied the file ID correctly (no extra spaces).

Wait a minute and refresh—Google Drive thumbnails can be slow the first time.

If it still fails, use a custom image (see below).

## CUSTOM PREVIEW IMAGE
Google Drive can generate a thumbnail for many videos automatically. If yours is blurry, shows the wrong frame, or does not load, you can use your own picture instead.

Take a screenshot of your video (pause on a good frame).

Upload that image in Hostinger's media library (or host it anywhere public).

In the code, find the line that starts with:

<img src="https://drive.google.com/thumbnail?id=

Replace that whole URL with your image URL, for example:

<img src="https://yourwebsite.com/images/my-video-poster.jpg"

Leave everything else the same. You still only change the image address—not the iframe or the script.

## IF ALIGNMENT IS OFF AFTER USING
Adjust only this one line inside the mobile section (@media max-width 768px):

transform: translate(-50%, -50%);

Try values like:

translate(-50%, -50%) for exact center.

translate(-50%, -60%) to move the video up more.

translate(-50%, -40%) to move it down more.

## IF YOU CLICK PLAY AND NOTHING HAPPENS
Some website builders remove <script> tags for security. This embed needs the small script at the bottom to swap the preview for the player.

Try a different Hostinger block type that allows custom HTML with scripts.

Paste the code again and make sure the <script> ... </script> section is still there after you save.

If Hostinger strips it every time, contact their support and ask how to add custom JavaScript on your plan.

CODE REVIEW (WHAT EACH PART MEANS)
video-shell is the outer box. It sets the maximum width, centers the embed on the page, rounds the corners, and clips anything that sticks out.

video-poster is the clickable preview layer. It holds your preview image and the play button. Visitors see this first.

video-play is the white triangle inside the circle. It is drawn with CSS, not an image file, so you do not need to upload a play icon.

video-iframe is the real Google Drive player. It stays hidden until someone clicks the poster.

YOUR_FILE_ID appears twice on purpose: once for the preview image link, once for the video player link.

The script at the bottom listens for a click, loads the iframe address from data-src, hides the poster, and shows the player.

Adjust your aspect ratio and maximum width as needed. I found that 4 / 3 works best.

## WHY THIS WORKS
Google Drive embeds are not as flexible as a direct MP4 video or a dedicated video host. Because of that, you usually cannot fully control the embedded player itself, but you can control its container—and what visitors see before the player loads.

When you drop a Drive iframe directly on a page, many browsers show a blank or black area until the user interacts. That is normal for Drive, not a mistake in your site. This fix does not change Drive's player; instead, it shows a picture first and only loads the iframe when someone wants to watch.

Google Drive embeds can behave differently on mobile browsers, so a manual transform on the iframe usually gives you more control than trying to rely on the player's internal layout. Responsive iframe patterns use a positioned wrapper, while transforms are the standard CSS way to line up the center of an element with the center of its parent.

## ADDITIONAL INFORMATION
The iframe is absolutely positioned and translated so its center lines up with the center of the frame.

The mobile media query shifts the iframe upward on phones, which helps fix the off-center look often seen on small screens.

The preview image uses Google's thumbnail service (thumbnail?id=...). It is tied to the same file ID as your video, so you usually do not need a separate image file.

This is best for situations where the video is stored in Google Drive and you want a polished embedded display without switching to a different hosting platform. It is especially useful when you need a responsive layout, rounded corners, a visible preview before play, and better mobile alignment while keeping the original Drive source.
