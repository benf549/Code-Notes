Grayson Work:
(12/28/2021) 8pm - 11pm

- Worked on designing the homepage
  - added the original slide show pictures to my rewrite
  - Added a twitter feed and placeholder for youtube video
  - created a page for the people section with placeholder images.

(12/29/2021) 2:30pm - 5:00pm

- Worked on the homepage

  - Added styling to neatly place the youtube video placeholder and twitter link next to eachother
  - Tweaked font styling and page spacing to accommodate hyperlinking.
  - Ensured the media box is responsive for mobile view

- Worked on the people page
  - Created a new javascript function which can pull out a hidden bio from the html and display it next to the person.
    - need to add actual people, but I want to see what dr. grayson thinks of this implementation
  - Used css grid and add bio-box to the grid and remove other element when clicked
    - Need to work on a way to hide/click off of the bio-box
    - Need to work on how grid displays for smaller screens.

(12/30/2021) 3:45 - 4:45

- Added a return button one a person's bio is shown.
- Updated slideshow javascript to have clickable photo-selectors.

(1/3/2021) 3:30 - 6:30

- Fixed mobile view for people page
- Copied and reformatted all publications from old website's publications page
- Created a footer with contact information which scales with screen size

(1/3/2021) 7:30 - 10:00

- Copied over Book Chapters from old website's publications tab

- Create research tab
  - reformatted text from original website
  - created photogrids to display images relevant to content of each text block.
    - Photogrids scale for small screen sizes
- Create a teaching section on the about page
  - copied and reformatted teaching content from old website.

(1/4/2021) 7:00 - 9:30

- Updated the people javascript code to allow full blocks of code to be injected into the biopopup which should allow for better styling
- Added all the post-docs with their images to the people page of the website.

(6/2/2022) 12:45pm - 2:45pm

- Add more students to people tab: (All Postdocs, PhD students, MS/Bachelors students)
- Need graduation years for Wonhee
- Need Ernesto, Nehali Bio
- Need updated Grayson Bio
- Fix Renee Liu -> Renee Nerenberg

(6/10/2022) 6:00pm - 8:00pm

- Add photos and teaching pages (needs content)
- Fix squashed photos on people page.
- Make about page slideshow scale better on mobile
- Add a Journal Articles and Book Chapters selector to the research tab to separate the information. (Need selectors by year).
- Make a year selector with scroll on the publications page that takes you to a given year's publications.
- Add new publications from grayson's email. (check order is correct).

(06/16/2022) 5:30pm - 7:00pm

- Update publications with fixed numbering scheme and other updates as per Grayson's email.
- Add Google Scholar and PubMed profile links to the top of publications page.
- Update Ernesto's bio, last names, and center long names on people page.
- Add lab alumni to the bottom of people page.
- Update teaching page course numbers and outreach activities.
- Rename photos page to gallery on all pages.
- Add Nehali bio.

(6/30/2022) 1:45pm - 3:30pm

- Add selectors for different groups of photos to gallery
- Add photo groups to hold thumbnails for the gallery images
- Add lighten effect on hover to gallery thumbnails
- Started copying over photos from the old website and from grayson's emails, need to implement a way to view them.

(7/7/2022) 1:30pm - 2:30pm

- Replace about page slideshow with GIF of lab group.
- Add links to gallery page selectors and create html pages for each subcategory.
- Ran the following to create a gif with FFMPEG.

```bash
ffmpeg -ss 00:00:00.000 -i 349F3C22-171F-46A8-A240-F387D9B9DBE1\ \(1\).MOV -pix_fmt rgb24 -r 10 -s 1280x960 -t 00:00:10.000 output.gif
```

(7/7/2022) 4:00pm - 6:30pm

- Design basic flex grid template to hold gallery photos, and add all previous group photos that I have been given.
- Make the header logo scale less dramatically when resizing the window
- Adjusted the sizing of front page ted talk video on front page as well as the twitter feed to be more readable on mobile/small screens.

(7/9/2022) 9am - 12am

- Add photos to gallery pages for graduations and goodbyes, holidays, and thanksgiving dinners sub-pages.
- Add gray color to the currently selected gallery sub-page to indicate which you're currently on.
- Add light gray highlight to gallery sub-page selectors and to people pages on mouse-hover.
- Add all event-photos from the previous website and labCOTE anniversary photos from grayson's email.

(7/14/2022) 2:30pm - 4:00pm

- Clip video of lab research for research page
- Used ffmpeg to convert clipped videos to GIFs
- Updated research image grids to use GIF videos and selected Recoolest pictures.

(7/15/2022) 2:30pm - 5:00pm

- Meet with Grayson to discuss next week's tasks
- Rename teaching page to impact page
- Remove lexi from people page
- Adjust footer to look nicer on smaller screens
- Add bone research gif
