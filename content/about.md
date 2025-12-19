---js
const eleventyNavigation = {
	key: "About",
	order: 3
};
---
# About

<div class="about-me">
	<p>
	Hi!
	<p>
	I'm Emily, a computer programming student at Raritan Valley Community College.
	<p>
	This website's purpose was to experiment with image generation using Google Gemini. 
	It also serves as a personal fan site for one of my favorite shows, House M.D.
</div>

<div class="suggestion-box">
  <h2>Contact Me</h2>
  <form class="comment-box" method="POST" netlify="true">
    <label for="comment-name">Name</label>
    <input type="text" id="comment-name" name="name" placeholder="Your name">

		<label for="email">Email</label>
		<input type="text" id="comment-email" email="email" placeholder="Your email">

    <label for="comment-message">Comments</label>
    <textarea id="comment-message" name="message" rows="4" placeholder="I too am in this comment section"></textarea>
		
    <button type="submit">Submit</button>
  </form>
</div>
