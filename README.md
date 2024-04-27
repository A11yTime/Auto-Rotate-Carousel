## Accessibility Consideration of Auto Rotating Carousel
* There must be play/pause mechanism with keyboard accessibility
* Image as carousel slide should have proper alternative text.
### Terminology
* aria-live="polite/off": For screen reader to expose information of slide when polite with manual navigation and off when auto rotaton to avoid annoyance.
* Section: Create a role region to provide accessible name.
* aria-roledescription="carousel": Identifes the elements as carousel rather than a region.
* aria-label="...": Provides the name of the section.
* role="group": Creates group of elements
* role-description="slide": Identifes element as slides rather than a group.
