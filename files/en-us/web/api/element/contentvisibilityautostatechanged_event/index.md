---
title: "Element: contentvisibilityautostatechanged event"
slug: Web/API/Element/contentvisibilityautostatechanged_event
page-type: web-api-event
tags:
  - Event
  - Reference
browser-compat: api.Element.contentvisibilityautostatechanged_event
---

{{APIRef("CSS Containment")}}

The **`contentvisibilityautostatechanged`** event fires on any element with {{cssxref("content-visibility", "content-visibility: auto")}} set on it when it starts or stops being [relevant to the user](/en-US/docs/Web/CSS/CSS_Containment#relevant_to_the_user) and [skipping its contents](/en-US/docs/Web/CSS/CSS_Containment#skips_its_contents).

While the element is not relevant (between the start and end events), the user agent skips an element's rendering, including layout and painting, which can significantly improve page rendering speed.
The {{domxref("element/contentvisibilityautostatechanged_event", "contentvisibilityautostatechanged")}} event provides a way for an app's code to also start or stop rendering processes (e.g. drawing on a {{htmlelement("canvas")}}) when they are not needed, thereby conserving processing power.

Note that even when hidden from view, element contents will remain semantically relevant (e.g. to assistive technology users), so this signal should not be used to skip significant semantic DOM updates.

## Syntax

Use the event name in methods like {{domxref("EventTarget.addEventListener", "addEventListener()")}}, or set an event handler property.

```js
addEventListener("contentvisibilityautostatechanged", (event) => {});
contentvisibilityautostatechanged = (event) => {};
```

> **Note:** The event object is of type {{domxref("ContentVisibilityAutoStateChangedEvent")}}.

## Examples

```js
const canvasElem = document.querySelector('canvas');

canvasElem.addEventListener('contentvisibilityautostatechanged', stateChanged);
canvasElem.style.contentVisibility = "auto";

function stateChanged(event) {
  if (event.skipped) {
    stopCanvasUpdates(canvasElem);
  } else {
    startCanvasUpdates(canvasElem);
  }
}

// Call this when the canvas updates need to start.
function startCanvasUpdates(canvas) {
  // … 
}

// Call this when the canvas updates need to stop.
function stopCanvasUpdates(canvas) {
  // …
}
```

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- {{domxref("ContentVisibilityAutoStateChangedEvent")}}
- [CSS Containment](/en-US/docs/Web/CSS/CSS_Containment)
- The {{cssxref("content-visibility")}} property
- The {{cssxref("contain")}} property
