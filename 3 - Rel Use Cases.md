# Iframely Rel Use Cases

    <link rel="player"                                 // intended use case
    type="text/html"                                   // embed as iFrame
    href="//iframe.ly/bFbn"                            // with this src
    media="(min-width:100) and (min-height:100)"       // when these sizes are ok
    title="Open Web FTW!" />


The `rel` attribute of a link under [Iframely Protocol](http://iframely.com/oembed2) contains 
an array of supported use cases, implemented by the publisher.

The initial dictionary for possible `rel` values as well as a process to extend it are given below.


## Generic destination `rel` & `iframely`

`rel` primarily reflects the user experience, but may also indicate supplementary information, 
such as the platform a widget is published for.

Thus, Iframely protocol supports per-platform optimization for publishers, 
recognizing that consumers may impose additional and specific requirements for the widgets they opt to consume.

If you wish your widget to be consumed by [Iframely Open-Source Embeds Gateway](http://iframely.com/gateway), 
please lead the list of your widget's `rel`-s with `iframely` tag:

    <link rel="iframely player" .... />

Other consumers, especially those relying on [embeds whitelisting process](http://iframely.com/qa) of their own, 
may specify their own destination rels. 

For example, if Twitter or Facebook, choose to consume widgets in Iframely spec, 
they would request that `twitter` and `facebook` to be added to rels list explicitly.


## `player`

`player` rel is for media playback experiences and cover video, audio and presentation-type widgets. 

The general requirements and recommendations for players are similar to 
[Twitter Player Card](https://dev.twitter.com/docs/cards/types/player-card) with some flexibility:

 - The best user experience is the responsive widgets with only aspect ratio defined: `media="aspect-ratio: 4:3"`
 - Publishers can specify iframe widgets (`type="text/html"`), Flash (`application/x-shockwave-flash:`), or any of `video/...` or `audio/...` MIME types, but are encouraged to provide multiple links if they support multiple formats so that consumers may choose for user's device and network characteristics.
 - Publishers should add `autoplay` value to the `rel` list, if their widget starts the media playback on load of the widget. 
 - Publishers should add `mature` value to the `rel` list, if the widget contains mature subject matter.
 - The use of HTTPS is optional (yet recommended for better distribution). However, when source widget is hosted under HTTPS URI, the requirements are the same as for Twitter Player Card.

 
Example of [Coub](http://coub.com) publishing [player](http://coub.com/view/2pc24rpb):

    <link rel="iframely player" href="https://coub.com/embed/2pc24rpb" type="text/html" 
     title="PARADISE BEACH"  media="(aspect-ratio: 1280:720)"/>
    
    <link rel="iframely player autoplay" href="http://c-cdn.coub.com/fb-player.swf?coubID=2pc24rpb" 
     type="application/x-shockwave-flash" title="PARADISE BEACH"  media="(aspect-ratio: 1280:720)"/>
    

[Preview the widget](http://iframe.ly/bF9Z).


## `image`

`image` is for photos, illustrations and inforgraphics and similar graphical content.

The intended use of an `image` is in the photo albums and galleries. It should be a primary content of the original page. 

For example, number of blogs and news sites optimize for Twitter platform by publishing 
photo card for their articles. Such approach is disapproved. 

Initially, the `image` should be accompanied by `image/..` MIME type and `sizes` attribute. 
However, it is expected that other MIME types be required in near future. (See how to extend below).


## `reader`



## `survey`

`survey` rel is for widgets asking user's opinion. 

The questionnaire should give sufficient context and load in a widget step-by-step so that user can spend as little time on answering the poll.


Example of [SlimSurveys](http://slimsurveys.com) publishing [survey](https://slimsurveys.com/s/eff75e32):

    <link rel="iframely survey" type="text/html" 
    href="https://slimsurveys.com/survey/eff75e32/embed" 
    media="(height: 250px) and (width: 300px)" title="UrbanEscape" />

[Preview the widget](http://iframe.ly/bFsC).


## `thumbnail`

Thumbnail images are the most popular among consumers and are used as a quick visual preview of the main content on publisher's page.

Publishers are encouraged to provide multiple `thumbnail` links, with varying image dimensions.

`thumbnail` should be used along `image/...` subset of MIME types and 
should be accompanied with `sizes` attribute to make it easier for consumers to choose which thumbnail to present to the user, given the device and network characteristics. 


## `logo`

Logo is given by publishers so that consumers may attribute a web link back to the original site. 

`logo` should be used along `image/...` subset of MIME types. 

Publishers should assume their logo will be used on light background (not necessarily white, 
so transparent logo background should be used), and should make their logo text readable to the user.

Here's [GitHub](https://github.com/) example:

    <link rel="logo" type="image/svg" 
    href="https://github-media-downloads.s3.amazonaws.com/github-logo.svg" />
    

## `icon`

Favicons are used to visually attribute the content to the publisher's webpage. 
They are usually used by consumers in junction with `href` containing the title of the page, or the publisher's site name.

`icon` rels already exist on most of the web pages, used by web browsers, 
and thus are grandfathered into Iframely protocol from [HTML5](http://www.w3schools.com/tags/tag_link.asp). 

Please, note that as of [HTML5](http://www.w3schools.com/tags/att_link_sizes.asp), 
`icon` rel should also be accompanied with `sizes` attribute:

    <link rel="icon" href="favicon.png" sizes="16x16 32x32" type="image/png"> 
    <link rel="icon" href="icon.svg" sizes="any" type="image/svg+xml">


## Extending the dictionary

Iframely protocol is fairly flexible and extendible as to additional use cases, 
thanks to the fact that `rel` attribute may contain a list of values.

Please, feel free to [fork this spec on Github](http://github.com/itteco/oembed2) and pull-request additional values, describing the requirements for the user experience. 

The discussions of pull-requests may be necessary if there are other providers of similar content that may wish to contribute for the requirements. 
However, such additional requirements may also be added as an extra `rel` value which will go with the primary one.

For example, here are some of use cases that we see the need for community to take a lead on:

 - `playback` - for `player` indicating that widget supports JavaScript or `window.postMessage` API to control media playback. With the list of calls, similar to what [YouTube](https://developers.google.com/youtube/iframe_api_reference#Events), [Vimeo](http://developer.vimeo.com/player/js-api) and [Soundcloud](http://developers.soundcloud.com/docs/api/html5-widget) have. 
 - `responsive` for `image`. The good coverage on the topic is [provided here](http://css-tricks.com/which-responsive-images-solution-should-you-use/).

Please, note that `mobile` versus `desktop` are not envisioned to be part of the `rel` in the future, but rather be put into `media` part of the link tag.





