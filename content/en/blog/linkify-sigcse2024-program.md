---
date: 2024-03-20
title: "Link-ify the SIGCSE Program for Great Good"
linkTitle: "link-ify sigcse program"
description: "The SIGCSE web program has onclick instead of href..."
---

# Use anchor tags if you're making a hyperlink

Assistive Tech Developers are just the best.
In the hellscape that is the web, they manage to do amazing things.
Let's help a pal out and follow web standards and accessibility guidelines whenever possible.

## Scenarios

There are 2 scenarios that I'm thinking of:
1. webdev wants to perform an action when the user clicks, uses an anchor tag without an href (which is invalid) and listens for the click event. This one seems to be covered all over the web. I'm a North Carolinian... sort of, so I'll just link [NC State on this one](https://accessibility.oit.ncsu.edu/it-accessibility-at-nc-state/developers/accessibility-handbook/mouse-and-keyboard-events/links/link-behavior/).
1. webdev has code that mostly does a bunch of other things great, doesn't want to break a bunch of old code and style, but does want to be able to link out to another page, so they apply a click handler that updates the `window.location` turning some non-anchor element into a link.

## Link-ifying the SIGCSE 2024 web program

The SIGCSE 2024 web program has a bunch of these. I'm fearful of falling for [the fallacy of Chesterson's Fence](https://en.wiktionary.org/wiki/Chesterton%27s_fence) or whatever, so I'll mention it to the organizers (do you think I hit up the Universal Design Chairs or the Web and Data Chairs? WHY NOT BOTH?! 😆). In the meantime I have a little userscript

```javascript
document.querySelectorAll('.search-result[onclick^="location.href="]').forEach((searchResult) => {
  const header = searchResult.getElementsByTagName('h4')[0]
  const loc = searchResult.getAttribute('onclick').match(/.+'([^']+)'/)[1]
  const inner = header.innerHTML
  if (loc && inner) {
  searchResult.removeAttribute('onclick')
    header.innerHTML = `<a target="_blank" rel="noopener noreferrer" href="${loc}">${inner} <i class="glyphicon glyphicon-new-window"></i></a>`
  }
})
```

but if userscripts aren't your bag, maybe bookmarklets are? you can drag the following to your bookmark toolbar then click it while on the SIGCSE web Program search results pages to have links that you can run down opening in the background if you press your magic hotkeys or just open in a tab for you if you basic click them.

<a href="javascript:document.querySelectorAll('.search-result[onclick^=\'location.href=\']').forEach((searchResult) => {const header = searchResult.getElementsByTagName('h4')[0];const loc = searchResult.getAttribute('onclick').match(/.+'([^']+)'/)[1];const inner = header.innerHTML;if (loc && inner) {searchResult.removeAttribute('onclick');header.innerHTML = `<a target='_blank' rel='noopener noreferrer' href='${loc}'>${inner} <i class='glyphicon glyphicon-new-window'></i></a>`;}})">Link-ify SIGCSE Program Search Results</a>