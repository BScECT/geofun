# Geodata Fundamentals' Textbook

This repository contains the source code for the [interactive textbook of Geodata Fundamentals](https://bscect.github.io/geofun). Geodata Fundamentals is a course taken by the first year students of the bachelor's degree program *Earth, Climate and Technology* (EC&T) at the Civil Engineering and Geosciences faculty of Delft University of Technology.

## Contributors
- Guillaume Rongier
- Paula Rulff
- Cornelis Slobbe
- Sandra Verhagen

## Reuse content
Feel free to reuse this content or contribute to it. Please give appropriate credit, provide a link to the license, and indicate if changes were made ([CC BY 4.0 License](https://creativecommons.org/licenses/by/4.0/))

The website (`<book_website_url>`) is created using the [TeachBooks Python package](https://github.com/TeachBooks/TeachBooks). To recreate it you have two options (more information in the [TeachBooks manual](https://teachbooks.io/manual/):
- In the GitHub interface: fork this repository, enable Github Pages from the source GitHub actions (Settings - Code and automation - Pages - Build and deployment - Source - GitHub Actions), enable workflows (Actions - I understand my workflows, go ahead and enable them) and run the call-deploy-book workflow (Actions - call-deploy-book - Run workflow - Run workflow). The website is released on the URL as shown on the workflow summary when the workflow has finished (Actions - call-deploy-book - call-deploy-book - Summary).
- On your own computer: clone this repository, install the required packages (`pip install -r requirements.txt`) and build the book (`teachbooks build book`). The website is stored locally in `book/_build/index.html`.
