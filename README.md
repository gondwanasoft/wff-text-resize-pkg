# wff-text-resize-pkg

A simple Watch Face Format element for testing the [Clockwork](https://clockwork-pkg.pages.dev/) and [XML Preprocessor](https://github.com/gondwanasoft/xml-preprocessor) Wear OS Watch Face Format (WFF)  utilities.

The element is like a simplified WFF `<Text>` element except that it adapts its font size so that the text always fits within its parent element, even when the text string changes length at run-time.

This document assumes familiarity with [Clockwork](https://clockwork-pkg.pages.dev/) and [XML Preprocessor](https://github.com/gondwanasoft/xml-preprocessor).

## Limitations

`wff-text-resize-pkg` is for testing Clockwork and XML Preprocessor; it is not expected to be sufficient for production use.

Most WFF text formatting options are not directly supported.

Text strings longer than seven characters will be ellipsized.

Due to WFF limitations, each instance of `wff-text-resize-pkg` will create eight complete `<PartText>` elements in your project. This will have an effect on size and possibly performance.

The `SYNC_TO_DEVICE` font family is assumed.

String length calculations are based on the assumption that '2' is the widest character.

## Installation

[Install Clockwork](https://clockwork-pkg.pages.dev/install).

Using Clockwork, [install XML Preprocessor](https://clockwork-pkg.pages.dev/guides/packages):

    clockwork install xml-preprocessor

Using Clockwork, [install wff-text-resize-pkg](https://clockwork-pkg.pages.dev/guides/packages):

    clockwork install https://github.com/gondwanasoft/wff-text-resize-pkg

## Usage

[Import](https://github.com/gondwanasoft/xml-preprocessor?tab=readme-ov-file#import) the package into your project's watchface-pp.xml:

    <Import href="../packages/wff-text-resize-pkg/text-resize.xml" />

A `textResize` element expands to a `<Group>`, so you can [`<Use>`](https://github.com/gondwanasoft/xml-preprocessor?tab=readme-ov-file#symbol-and-use-elements) a `textResize` wherever you could put a `<Group>`.

In your `<Use>` element, you can include the following [custom attributes](https://github.com/gondwanasoft/xml-preprocessor?tab=readme-ov-file#customising-use-instances-with-top-level-attributes):

* `data-value="text"` where `text` is the string to display

* `data-color="color"`

* `data-align="alignment"`

Here's a simple example:

    <Use
        href="textResize"
        x="0"
        y="0"
        width="{PARENT}"
        height="{PARENT}"
        data-value="'round(pow(10,[SECOND]%8))'"
        data-color="'#00ff00'"
        data-align="'END'"/>

textResize is probably most useful for displaying complication text and title; _eg_, using `data-value="'[COMPLICATION.TEXT]'"`.