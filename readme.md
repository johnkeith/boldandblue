## Bold and Blue Octopress Theme

Bold and Blue is an Octopress theme designed to be bold, but minimal.

![Bold and Blue](http://gdurl.com/GYDa)

For a demo, head [this way](http://www.johnkeith.us).

To get this snazzy fellow running on your blog, follow the instructions below.
 
Navigate to the root of your Octopress install, then run these two commands.

	$ git clone https://github.com/johnkeith/boldandblue.git .themes/boldandblue
		
	$ bundle exec rake install['boldandblue']

Or, if zsh is giving you grief, use this instead of the previous line.
		
	$ bundle exec rake install\['boldandblue'\]

Tada! That's all folks - read on only if you want to see the rational behind some of Bold and Blue's design decisions.

## Whys and Wherefores of the Design

Octopress' basic theme does a great job with many aspects: layout, typography, and responsiveness. (In short, readability is the base design's strong suit). What it lacks, however, is pizzaz.

This theme aims to add a little boldness to the mix, while retaining the spirit of what makes Octopress a user-friendly and recognizable platform. 

Bold and Blue changes the default Octopress fonts. The default serif stack is now `$serif: "Noto Serif", serif;` and the default sans stack is `$sans: "Open Sans", sans-serif;	`. The heading font family uses the sans stack. 

Color is also altered in this theme, but only slightly. Under sass/custom/_colors.scss you can see the changes that were made in order to strip out the darkness and textures of the default Octopress theme. This new theme utilizes Octopress's grey defaults for the majority of the typography, but it adds an accent color that can be seen in the site title and all links. This accent can easily be changed - simply alter the value of `$link-color` in the _colors.scss file and this will change the colors in the navbar, the title, and even the text in the search box. 

Typographically, a few changes were made. Due to the increased width of the body (1320px max as opposed to the 1200px max of Octopress' defaults), the line-height and font-size of the body element have been increased to 1.8em and 1.1em respectively. (You can see this change in sass/custom/_styles.scss). 

Bold and Blue also incorporates a sticky header. While I may try to animate the header's sticking process at some point in the future, for now I think the transition is fine, due to the white background of both header and body. The jQuery that enables the sticky header can be found in the source/_includes/custom/after_footer.html, while the CSS that keeps the header where it needs to be is in the _styles.scss file. (The jQuery and CSS snippets for this header came from [this article](http://www.hongkiat.com/blog/css-sticky-position/)).

Additionally, the site search box has been moved into the sidebar, due to the fixed position of the header. Additionally, the RSS icon has been commented out, like the search box, in the source/_includes/navigation.html file. You can find the new location of the search box in source/_includes/index.html.

Finally, material in the sidebar has been seperated into its own file - source/_includes/aside.html. This file is then included in the source/index.html, source/_layouts/page.html, and source/_layouts/post.html.

