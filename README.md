# Custom-Video-Embed-Formatting
TLDR: Use on customizable websites such as Hostinger and Wordpress to avoid broken "video URL" errors. It will even round your courners.

OVERVIEW
This code solves a common issue when embedding a Google Drive-hosted video inside a website builder like Hostinger: the video may display correctly on desktop, but look misaligned on mobile, lose its rounded-corner crop, or refuse to sit centered inside the visible frame. The solution uses a wrapper element to control the visible crop area and positions the embedded iframe so the video stays centered and visually consistent across screen sizes.

This embed is designed to display a Google Drive-hosted video in a responsive, cropped frame with rounded corners. The wrapper controls the size and positioning of the video so it stays centered on desktop and mobile, but the interactive playback controls still depend on Google Drive’s embedded player, which can behave inconsistently on mobile browsers.

WHAT THIS CODE DOES
Creates a fixed aspect-ratio video box for a clean desktop layout.

Uses overflow: hidden and border-radius to crop the video with curved edges.

Centers the iframe inside the box with CSS positioning and transforms.

Expands and nudges the video slightly on mobile so the visible part stays better aligned.

Keeps the embed responsive so it scales down naturally on smaller screens.

IF ALIGNMENT IS OFF AFTER USING
Adjust only this one line on mobile:

transform: translate(-50%, -50%);

Try values like:

translate(-50%, -50%) for exact center.

translate(-50%, -60%) to move the video up more.

translate(-50%, -40%) to move it down more.

WHY THIS WORKS
Google Drive embeds are not as flexible as a direct MP4 video or a dedicated video host. Because of that, you usually cannot fully control the embedded player itself, but you can control its container. This approach works by styling the container to manage size, crop, and positioning, which gives a much better result than relying on the default embed alone.

Google Drive embeds can behave differently on mobile browsers, so a little oversizing plus a manual transform usually gives you more control than trying to rely on the player’s internal layout. Responsive iframe patterns use a positioned wrapper, while transforms are the standard CSS way to line up the center of an element with the center of its parent.

WALKTHROUGH
Open Google Drive, find your video, and remove all sharing restrictions (ie Anyone on the internet with the link can view).

Copy your link and add it into the "src=" section. It should look something like this: src="https://drive.google.com/file/d/123456789xyz/preview"

On Hostinger, add a new code <> element

Add your code and adjust the settings according to your prefences.

CODE REVIEW
video-shell sets the maximum width and centers the whole embed on the page.

video-frame defines the visible video window, applies rounded corners, and hides overflow so the iframe gets clipped cleanly.

Adjust your aspect ratio and maximum width as needed. I found that 4 / 3 works best.

ADDITIONAL INFORMATION
The iframe is absolutely positioned and translated so its center lines up with the center of the frame.

The mobile media query adjusts the crop slightly by making the iframe a bit larger and shifting it upward, which helps fix the off-center look often seen on phones.

This is best for situations where the video is stored in Google Drive and you want a polished embedded display without switching to a different hosting platform. It is especially useful when you need a responsive layout, rounded corners, and better mobile alignment while keeping the original Drive source.