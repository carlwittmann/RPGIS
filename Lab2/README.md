# Terra Incognita

*Abstracting Cartography, Childhood Novels, and Fantasy Maps*

| <img src="https://github.com/carlwittmann/RPGIS/blob/main/pics/100acrewoods.jpg" height="300px"> | <img src="https://www.lancaster.ac.uk/dighum/files/2016/09/1936map-1024x765.jpg" height="300px"> | <img src="https://www.bl.uk/britishlibrary/~/media/bl/global/maps/collection%20items/6%20map%20of%20the%20middle%20earth.jpg" height="300px"> |
| :------: | :------: | :------: |
| *The 100 Acre Woods* | *The Lake District* | *Middle Earth* |

*(Link to map: https://carlwittmann.github.io/RPGIS/)*

If I had to pinpoint where it all started, it would be here: Christopher Robin's 100 Acre Woods, the Lake District as imagined by the Swallows & Amazons, and Tolkein's Middle Earth. I spent a lot of time in libraries as a child; throughout the '90s in Riyadh, there was exactly one store that sold English novels - Jarir Bookstore - and selection was limited. The libraries at the American International School, however, were *stacked to the roof* with books. It is difficult to understate just how important those libraries were to me - the novels I read sitting on that worn industrial carpet between shelves played a significant part in shaping who I am today. I can remember the sound of basketballs outside while other kids were at recess, the way the small dusty windows filtered the midday desert sun, the way the waterfountain tasted, the first time I skipped class (after pulling my first Discworld novel off the shelf)... and I remember looking for maps. I remember going book by book down the aisles, flipping through the first few pages, and collecting stacks of novels that began with a map.

I was obsessed with those maps. I spent hours pouring over them, imagining what might be and what might have been. As I read through the novels, I constantly referenced the maps. I started drawing my own maps to extend the world beyond the borders of the printed page. I was absolutely captivated.

Looking back, I can't help but ponder the dichotomy between the maps I was drawn to as a child and the maps I produce as an aspiring geospatial professional. I fell in love with maps not for the questions they answered, but for the questions they posed, yet when I personally approach a cartographic task I feel compelled to produce a nearly-infallible document - after all, shouldn't that be the goal of a cartographer? It certainly was drilled into me over the course of my degree, and I began to view everything I do through an empirical lens: If I want to be taken seriously, I should make serious maps. 

Over this past semester, I've started to realize that I may have limited myself somewhat in that regard. I've forgotten that maps can be fun, or artistic, or playful. This lab was an opportunity for me to take a step back and reflect upon the maps which first sparked my interest in cartography, and which ultimately led to this essay.

In the planning phase of this project, (and at your recommendation,) I spent a significant amount of time browsing through Erwin Raisz's *General Cartography* (1948) along with all of my favourite fantasy maps (a selection of which are displayed at the top of the page). In the technical portion of the project, I gained a great amount of insight from discussions between OpenStreetMap contributors, in particular [this thread](https://github.com/gravitystorm/openstreetmap-carto/issues/938) on methods of randomizing forest icons, which culminates in Cristoph Hormann's [pattern generation tool](http://www.imagico.de/map/jsdotpattern.php). (I actually forked the repository and spent quite a bit of time trying to load it with custom .svg icons, but never quite got that figured out.)

Early on, it was clear that I was going to have to be creative in my use of polygons - the map loses a certain *je ne sais quoi* when the geography is too detailed. I think this is largely due to the human propensity for pattern recognition - as soon as the eye notices a familiar coastline, for example, the spell is broken, and when that spell is broken, our brain stops filling in the gaps with imagination and starts trying to fit in "known" information. It's almost like an optical illusion. For these reasons, most basemaps (and *any* administrative boundaries) were not suitable. Fortunately, I already had the land linework in my back pocket - I found [Dylan Moriarty's hand-drawn basemap](https://dylanmoriarty.github.io/blog/moriarty-hand.html) years ago, and use it extensively for inset maps. It was the perfect fit for this project and I immediately knew that it was going to be the canvas for the rest of the map.

For the pattern symbology, I used a combination of Christoph Hormann's pattern generator and Inkscape to create .svg icons out of Erwin Raisz's mountain range symbology. At first, though, the patterns were too uniformly distributed - they were pleasantly randomized, but there was no empty space! I specifically used the pattern generator "shake" function to form clusters of icons, and then I edited the .svg tiles further in Inkscape to remove icons and create space for the imagination to wander. I also used the pattern generator to create tiles for the pin-point stippled effect which overlays the entire map.

The next challenge was figuring out how to apply the symbology within Mapbox. I decided to use a global bioregion shapefile (clipped to the Moriarty linework), which distributed the patterns across the landcover in a very natural and organic fashion. Pattern symbology was matched to the attribute table of the bioregions. 

The interactive portion of the project was geared towards giving the user tools to make the map useful to their own purposes. The hex grid is a classic mechanic for facilitating long-distance travel in tabletop RPGs; I made the scale adjustable because the truth is that on this map, scale doesn't matter - it's whatever you declare it to be. The mirror mode was included to add an extra twist of the unknown by making the familiar unfamiliar, and the parchment effect was added via CSS for reasons that at this point I assume are rather obvious. Unfortunately, these interactive portions were implemented *over* the map with CSS and p5.js, so changes made to the hex grid, mirror mode, and parchment overlay are not reflected in the next interactive element that I added, a "Download as PDF" plugin for Mapbox GL JS that allows users to save a high-quality image of the map. Finally - and mostly because I was worried that it wasn't interactive enough yet - I added an optional icon that users can add to the map if they want to use this for, say, a game of D&D. The icons placed by users are exported with the pdf, which is nice. 

In terms of UI, I went through several iterations of button layout and title before settling on a single row across the top. (Visually, I think they looked better at the bottom, but they weren't immediately noticeable. They're easier to see up top.) I styled the clickable buttons with a satisfying little "push" animation just for fun. I also added a (different) parchment background to the webpage, and applied a color blend mode via CSS to the buttons so that they thematically matched the rest of the map. Finally, I found a little scroll banner for the title to give it a bit of whimsy.

I'm pretty happy with how it turned out! I actually plan on remaking this in the future, but instead of using tiled patterns I will multiple layers (for different zoom levels) of points randomized within their polygons. It should be easy to implement the parchment texture within Mapbox as a proper layer so that it renders to PDF, too. I'd also like to add more icons.

The best part is that I had a lot of fun making this. It was rewarding and very, very nostalgic. Honestly, I think I'm going to continue making fantasy maps for fun.


| <img src="https://github.com/carlwittmann/RPGIS/blob/main/pics/normal.png" height="300px"> | <img src="https://github.com/carlwittmann/RPGIS/blob/main/pics/mirror_parchment.png" height="300px"> |
| :------: | :------: |
| Normal View | Mirror + Parchment |


| <img src="https://github.com/carlwittmann/RPGIS/blob/main/pics/exportview_issues.png" height="500px"> | <img src="https://github.com/carlwittmann/RPGIS/blob/main/pics/export.png" height="500px"> |
| :------: | :------: |
| View Before Export | Exported Image |
