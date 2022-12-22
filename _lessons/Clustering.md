---
layout: page
title: Clustering with Scikit-Learn
description: This lesson uses Scikit-Learn to cluster data.
---

<html>
<head><meta charset="utf-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>ClusteringScikitLearn</title><script src="https://cdnjs.cloudflare.com/ajax/libs/require.js/2.1.10/require.min.js"></script>




<style type="text/css">
    pre { line-height: 125%; }
td.linenos .normal { color: inherit; background-color: transparent; padding-left: 5px; padding-right: 5px; }
span.linenos { color: inherit; background-color: transparent; padding-left: 5px; padding-right: 5px; }
td.linenos .special { color: #000000; background-color: #ffffc0; padding-left: 5px; padding-right: 5px; }
span.linenos.special { color: #000000; background-color: #ffffc0; padding-left: 5px; padding-right: 5px; }
.highlight .hll { background-color: var(--jp-cell-editor-active-background) }
.highlight { background: var(--jp-cell-editor-background); color: var(--jp-mirror-editor-variable-color) }
.highlight .c { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment */
.highlight .err { color: var(--jp-mirror-editor-error-color) } /* Error */
.highlight .k { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword */
.highlight .o { color: var(--jp-mirror-editor-operator-color); font-weight: bold } /* Operator */
.highlight .p { color: var(--jp-mirror-editor-punctuation-color) } /* Punctuation */
.highlight .ch { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.Hashbang */
.highlight .cm { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.Multiline */
.highlight .cp { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.Preproc */
.highlight .cpf { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.PreprocFile */
.highlight .c1 { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.Single */
.highlight .cs { color: var(--jp-mirror-editor-comment-color); font-style: italic } /* Comment.Special */
.highlight .kc { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Constant */
.highlight .kd { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Declaration */
.highlight .kn { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Namespace */
.highlight .kp { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Pseudo */
.highlight .kr { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Reserved */
.highlight .kt { color: var(--jp-mirror-editor-keyword-color); font-weight: bold } /* Keyword.Type */
.highlight .m { color: var(--jp-mirror-editor-number-color) } /* Literal.Number */
.highlight .s { color: var(--jp-mirror-editor-string-color) } /* Literal.String */
.highlight .ow { color: var(--jp-mirror-editor-operator-color); font-weight: bold } /* Operator.Word */
.highlight .w { color: var(--jp-mirror-editor-variable-color) } /* Text.Whitespace */
.highlight .mb { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Bin */
.highlight .mf { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Float */
.highlight .mh { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Hex */
.highlight .mi { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Integer */
.highlight .mo { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Oct */
.highlight .sa { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Affix */
.highlight .sb { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Backtick */
.highlight .sc { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Char */
.highlight .dl { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Delimiter */
.highlight .sd { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Doc */
.highlight .s2 { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Double */
.highlight .se { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Escape */
.highlight .sh { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Heredoc */
.highlight .si { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Interpol */
.highlight .sx { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Other */
.highlight .sr { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Regex */
.highlight .s1 { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Single */
.highlight .ss { color: var(--jp-mirror-editor-string-color) } /* Literal.String.Symbol */
.highlight .il { color: var(--jp-mirror-editor-number-color) } /* Literal.Number.Integer.Long */
  </style>



<style type="text/css">
/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*
 * Mozilla scrollbar styling
 */

/* use standard opaque scrollbars for most nodes */
[data-jp-theme-scrollbars='true'] {
  scrollbar-color: rgb(var(--jp-scrollbar-thumb-color))
    var(--jp-scrollbar-background-color);
}

/* for code nodes, use a transparent style of scrollbar. These selectors
 * will match lower in the tree, and so will override the above */
[data-jp-theme-scrollbars='true'] .CodeMirror-hscrollbar,
[data-jp-theme-scrollbars='true'] .CodeMirror-vscrollbar {
  scrollbar-color: rgba(var(--jp-scrollbar-thumb-color), 0.5) transparent;
}

/* tiny scrollbar */

.jp-scrollbar-tiny {
  scrollbar-color: rgba(var(--jp-scrollbar-thumb-color), 0.5) transparent;
  scrollbar-width: thin;
}

/*
 * Webkit scrollbar styling
 */

/* use standard opaque scrollbars for most nodes */

[data-jp-theme-scrollbars='true'] ::-webkit-scrollbar,
[data-jp-theme-scrollbars='true'] ::-webkit-scrollbar-corner {
  background: var(--jp-scrollbar-background-color);
}

[data-jp-theme-scrollbars='true'] ::-webkit-scrollbar-thumb {
  background: rgb(var(--jp-scrollbar-thumb-color));
  border: var(--jp-scrollbar-thumb-margin) solid transparent;
  background-clip: content-box;
  border-radius: var(--jp-scrollbar-thumb-radius);
}

[data-jp-theme-scrollbars='true'] ::-webkit-scrollbar-track:horizontal {
  border-left: var(--jp-scrollbar-endpad) solid
    var(--jp-scrollbar-background-color);
  border-right: var(--jp-scrollbar-endpad) solid
    var(--jp-scrollbar-background-color);
}

[data-jp-theme-scrollbars='true'] ::-webkit-scrollbar-track:vertical {
  border-top: var(--jp-scrollbar-endpad) solid
    var(--jp-scrollbar-background-color);
  border-bottom: var(--jp-scrollbar-endpad) solid
    var(--jp-scrollbar-background-color);
}

/* for code nodes, use a transparent style of scrollbar */

[data-jp-theme-scrollbars='true'] .CodeMirror-hscrollbar::-webkit-scrollbar,
[data-jp-theme-scrollbars='true'] .CodeMirror-vscrollbar::-webkit-scrollbar,
[data-jp-theme-scrollbars='true']
  .CodeMirror-hscrollbar::-webkit-scrollbar-corner,
[data-jp-theme-scrollbars='true']
  .CodeMirror-vscrollbar::-webkit-scrollbar-corner {
  background-color: transparent;
}

[data-jp-theme-scrollbars='true']
  .CodeMirror-hscrollbar::-webkit-scrollbar-thumb,
[data-jp-theme-scrollbars='true']
  .CodeMirror-vscrollbar::-webkit-scrollbar-thumb {
  background: rgba(var(--jp-scrollbar-thumb-color), 0.5);
  border: var(--jp-scrollbar-thumb-margin) solid transparent;
  background-clip: content-box;
  border-radius: var(--jp-scrollbar-thumb-radius);
}

[data-jp-theme-scrollbars='true']
  .CodeMirror-hscrollbar::-webkit-scrollbar-track:horizontal {
  border-left: var(--jp-scrollbar-endpad) solid transparent;
  border-right: var(--jp-scrollbar-endpad) solid transparent;
}

[data-jp-theme-scrollbars='true']
  .CodeMirror-vscrollbar::-webkit-scrollbar-track:vertical {
  border-top: var(--jp-scrollbar-endpad) solid transparent;
  border-bottom: var(--jp-scrollbar-endpad) solid transparent;
}

/* tiny scrollbar */

.jp-scrollbar-tiny::-webkit-scrollbar,
.jp-scrollbar-tiny::-webkit-scrollbar-corner {
  background-color: transparent;
  height: 4px;
  width: 4px;
}

.jp-scrollbar-tiny::-webkit-scrollbar-thumb {
  background: rgba(var(--jp-scrollbar-thumb-color), 0.5);
}

.jp-scrollbar-tiny::-webkit-scrollbar-track:horizontal {
  border-left: 0px solid transparent;
  border-right: 0px solid transparent;
}

.jp-scrollbar-tiny::-webkit-scrollbar-track:vertical {
  border-top: 0px solid transparent;
  border-bottom: 0px solid transparent;
}

/*
 * Phosphor
 */

.lm-ScrollBar[data-orientation='horizontal'] {
  min-height: 16px;
  max-height: 16px;
  min-width: 45px;
  border-top: 1px solid #a0a0a0;
}

.lm-ScrollBar[data-orientation='vertical'] {
  min-width: 16px;
  max-width: 16px;
  min-height: 45px;
  border-left: 1px solid #a0a0a0;
}

.lm-ScrollBar-button {
  background-color: #f0f0f0;
  background-position: center center;
  min-height: 15px;
  max-height: 15px;
  min-width: 15px;
  max-width: 15px;
}

.lm-ScrollBar-button:hover {
  background-color: #dadada;
}

.lm-ScrollBar-button.lm-mod-active {
  background-color: #cdcdcd;
}

.lm-ScrollBar-track {
  background: #f0f0f0;
}

.lm-ScrollBar-thumb {
  background: #cdcdcd;
}

.lm-ScrollBar-thumb:hover {
  background: #bababa;
}

.lm-ScrollBar-thumb.lm-mod-active {
  background: #a0a0a0;
}

.lm-ScrollBar[data-orientation='horizontal'] .lm-ScrollBar-thumb {
  height: 100%;
  min-width: 15px;
  border-left: 1px solid #a0a0a0;
  border-right: 1px solid #a0a0a0;
}

.lm-ScrollBar[data-orientation='vertical'] .lm-ScrollBar-thumb {
  width: 100%;
  min-height: 15px;
  border-top: 1px solid #a0a0a0;
  border-bottom: 1px solid #a0a0a0;
}

.lm-ScrollBar[data-orientation='horizontal']
  .lm-ScrollBar-button[data-action='decrement'] {
  background-image: var(--jp-icon-caret-left);
  background-size: 17px;
}

.lm-ScrollBar[data-orientation='horizontal']
  .lm-ScrollBar-button[data-action='increment'] {
  background-image: var(--jp-icon-caret-right);
  background-size: 17px;
}

.lm-ScrollBar[data-orientation='vertical']
  .lm-ScrollBar-button[data-action='decrement'] {
  background-image: var(--jp-icon-caret-up);
  background-size: 17px;
}

.lm-ScrollBar[data-orientation='vertical']
  .lm-ScrollBar-button[data-action='increment'] {
  background-image: var(--jp-icon-caret-down);
  background-size: 17px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/


/* <DEPRECATED> */ .p-Widget, /* </DEPRECATED> */
.lm-Widget {
  box-sizing: border-box;
  position: relative;
  overflow: hidden;
  cursor: default;
}


/* <DEPRECATED> */ .p-Widget.p-mod-hidden, /* </DEPRECATED> */
.lm-Widget.lm-mod-hidden {
  display: none !important;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/


/* <DEPRECATED> */ .p-CommandPalette, /* </DEPRECATED> */
.lm-CommandPalette {
  display: flex;
  flex-direction: column;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}


/* <DEPRECATED> */ .p-CommandPalette-search, /* </DEPRECATED> */
.lm-CommandPalette-search {
  flex: 0 0 auto;
}


/* <DEPRECATED> */ .p-CommandPalette-content, /* </DEPRECATED> */
.lm-CommandPalette-content {
  flex: 1 1 auto;
  margin: 0;
  padding: 0;
  min-height: 0;
  overflow: auto;
  list-style-type: none;
}


/* <DEPRECATED> */ .p-CommandPalette-header, /* </DEPRECATED> */
.lm-CommandPalette-header {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}


/* <DEPRECATED> */ .p-CommandPalette-item, /* </DEPRECATED> */
.lm-CommandPalette-item {
  display: flex;
  flex-direction: row;
}


/* <DEPRECATED> */ .p-CommandPalette-itemIcon, /* </DEPRECATED> */
.lm-CommandPalette-itemIcon {
  flex: 0 0 auto;
}


/* <DEPRECATED> */ .p-CommandPalette-itemContent, /* </DEPRECATED> */
.lm-CommandPalette-itemContent {
  flex: 1 1 auto;
  overflow: hidden;
}


/* <DEPRECATED> */ .p-CommandPalette-itemShortcut, /* </DEPRECATED> */
.lm-CommandPalette-itemShortcut {
  flex: 0 0 auto;
}


/* <DEPRECATED> */ .p-CommandPalette-itemLabel, /* </DEPRECATED> */
.lm-CommandPalette-itemLabel {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}

.lm-close-icon {
	border:1px solid transparent;
  background-color: transparent;
  position: absolute;
	z-index:1;
	right:3%;
	top: 0;
	bottom: 0;
	margin: auto;
	padding: 7px 0;
	display: none;
	vertical-align: middle;
  outline: 0;
  cursor: pointer;
}
.lm-close-icon:after {
	content: "X";
	display: block;
	width: 15px;
	height: 15px;
	text-align: center;
	color:#000;
	font-weight: normal;
	font-size: 12px;
	cursor: pointer;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/


/* <DEPRECATED> */ .p-DockPanel, /* </DEPRECATED> */
.lm-DockPanel {
  z-index: 0;
}


/* <DEPRECATED> */ .p-DockPanel-widget, /* </DEPRECATED> */
.lm-DockPanel-widget {
  z-index: 0;
}


/* <DEPRECATED> */ .p-DockPanel-tabBar, /* </DEPRECATED> */
.lm-DockPanel-tabBar {
  z-index: 1;
}


/* <DEPRECATED> */ .p-DockPanel-handle, /* </DEPRECATED> */
.lm-DockPanel-handle {
  z-index: 2;
}


/* <DEPRECATED> */ .p-DockPanel-handle.p-mod-hidden, /* </DEPRECATED> */
.lm-DockPanel-handle.lm-mod-hidden {
  display: none !important;
}


/* <DEPRECATED> */ .p-DockPanel-handle:after, /* </DEPRECATED> */
.lm-DockPanel-handle:after {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  content: '';
}


/* <DEPRECATED> */
.p-DockPanel-handle[data-orientation='horizontal'],
/* </DEPRECATED> */
.lm-DockPanel-handle[data-orientation='horizontal'] {
  cursor: ew-resize;
}


/* <DEPRECATED> */
.p-DockPanel-handle[data-orientation='vertical'],
/* </DEPRECATED> */
.lm-DockPanel-handle[data-orientation='vertical'] {
  cursor: ns-resize;
}


/* <DEPRECATED> */
.p-DockPanel-handle[data-orientation='horizontal']:after,
/* </DEPRECATED> */
.lm-DockPanel-handle[data-orientation='horizontal']:after {
  left: 50%;
  min-width: 8px;
  transform: translateX(-50%);
}


/* <DEPRECATED> */
.p-DockPanel-handle[data-orientation='vertical']:after,
/* </DEPRECATED> */
.lm-DockPanel-handle[data-orientation='vertical']:after {
  top: 50%;
  min-height: 8px;
  transform: translateY(-50%);
}


/* <DEPRECATED> */ .p-DockPanel-overlay, /* </DEPRECATED> */
.lm-DockPanel-overlay {
  z-index: 3;
  box-sizing: border-box;
  pointer-events: none;
}


/* <DEPRECATED> */ .p-DockPanel-overlay.p-mod-hidden, /* </DEPRECATED> */
.lm-DockPanel-overlay.lm-mod-hidden {
  display: none !important;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/


/* <DEPRECATED> */ .p-Menu, /* </DEPRECATED> */
.lm-Menu {
  z-index: 10000;
  position: absolute;
  white-space: nowrap;
  overflow-x: hidden;
  overflow-y: auto;
  outline: none;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}


/* <DEPRECATED> */ .p-Menu-content, /* </DEPRECATED> */
.lm-Menu-content {
  margin: 0;
  padding: 0;
  display: table;
  list-style-type: none;
}


/* <DEPRECATED> */ .p-Menu-item, /* </DEPRECATED> */
.lm-Menu-item {
  display: table-row;
}


/* <DEPRECATED> */
.p-Menu-item.p-mod-hidden,
.p-Menu-item.p-mod-collapsed,
/* </DEPRECATED> */
.lm-Menu-item.lm-mod-hidden,
.lm-Menu-item.lm-mod-collapsed {
  display: none !important;
}


/* <DEPRECATED> */
.p-Menu-itemIcon,
.p-Menu-itemSubmenuIcon,
/* </DEPRECATED> */
.lm-Menu-itemIcon,
.lm-Menu-itemSubmenuIcon {
  display: table-cell;
  text-align: center;
}


/* <DEPRECATED> */ .p-Menu-itemLabel, /* </DEPRECATED> */
.lm-Menu-itemLabel {
  display: table-cell;
  text-align: left;
}


/* <DEPRECATED> */ .p-Menu-itemShortcut, /* </DEPRECATED> */
.lm-Menu-itemShortcut {
  display: table-cell;
  text-align: right;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/


/* <DEPRECATED> */ .p-MenuBar, /* </DEPRECATED> */
.lm-MenuBar {
  outline: none;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}


/* <DEPRECATED> */ .p-MenuBar-content, /* </DEPRECATED> */
.lm-MenuBar-content {
  margin: 0;
  padding: 0;
  display: flex;
  flex-direction: row;
  list-style-type: none;
}


/* <DEPRECATED> */ .p--MenuBar-item, /* </DEPRECATED> */
.lm-MenuBar-item {
  box-sizing: border-box;
}


/* <DEPRECATED> */
.p-MenuBar-itemIcon,
.p-MenuBar-itemLabel,
/* </DEPRECATED> */
.lm-MenuBar-itemIcon,
.lm-MenuBar-itemLabel {
  display: inline-block;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/


/* <DEPRECATED> */ .p-ScrollBar, /* </DEPRECATED> */
.lm-ScrollBar {
  display: flex;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}


/* <DEPRECATED> */
.p-ScrollBar[data-orientation='horizontal'],
/* </DEPRECATED> */
.lm-ScrollBar[data-orientation='horizontal'] {
  flex-direction: row;
}


/* <DEPRECATED> */
.p-ScrollBar[data-orientation='vertical'],
/* </DEPRECATED> */
.lm-ScrollBar[data-orientation='vertical'] {
  flex-direction: column;
}


/* <DEPRECATED> */ .p-ScrollBar-button, /* </DEPRECATED> */
.lm-ScrollBar-button {
  box-sizing: border-box;
  flex: 0 0 auto;
}


/* <DEPRECATED> */ .p-ScrollBar-track, /* </DEPRECATED> */
.lm-ScrollBar-track {
  box-sizing: border-box;
  position: relative;
  overflow: hidden;
  flex: 1 1 auto;
}


/* <DEPRECATED> */ .p-ScrollBar-thumb, /* </DEPRECATED> */
.lm-ScrollBar-thumb {
  box-sizing: border-box;
  position: absolute;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/


/* <DEPRECATED> */ .p-SplitPanel-child, /* </DEPRECATED> */
.lm-SplitPanel-child {
  z-index: 0;
}


/* <DEPRECATED> */ .p-SplitPanel-handle, /* </DEPRECATED> */
.lm-SplitPanel-handle {
  z-index: 1;
}


/* <DEPRECATED> */ .p-SplitPanel-handle.p-mod-hidden, /* </DEPRECATED> */
.lm-SplitPanel-handle.lm-mod-hidden {
  display: none !important;
}


/* <DEPRECATED> */ .p-SplitPanel-handle:after, /* </DEPRECATED> */
.lm-SplitPanel-handle:after {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  content: '';
}


/* <DEPRECATED> */
.p-SplitPanel[data-orientation='horizontal'] > .p-SplitPanel-handle,
/* </DEPRECATED> */
.lm-SplitPanel[data-orientation='horizontal'] > .lm-SplitPanel-handle {
  cursor: ew-resize;
}


/* <DEPRECATED> */
.p-SplitPanel[data-orientation='vertical'] > .p-SplitPanel-handle,
/* </DEPRECATED> */
.lm-SplitPanel[data-orientation='vertical'] > .lm-SplitPanel-handle {
  cursor: ns-resize;
}


/* <DEPRECATED> */
.p-SplitPanel[data-orientation='horizontal'] > .p-SplitPanel-handle:after,
/* </DEPRECATED> */
.lm-SplitPanel[data-orientation='horizontal'] > .lm-SplitPanel-handle:after {
  left: 50%;
  min-width: 8px;
  transform: translateX(-50%);
}


/* <DEPRECATED> */
.p-SplitPanel[data-orientation='vertical'] > .p-SplitPanel-handle:after,
/* </DEPRECATED> */
.lm-SplitPanel[data-orientation='vertical'] > .lm-SplitPanel-handle:after {
  top: 50%;
  min-height: 8px;
  transform: translateY(-50%);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/


/* <DEPRECATED> */ .p-TabBar, /* </DEPRECATED> */
.lm-TabBar {
  display: flex;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}


/* <DEPRECATED> */ .p-TabBar[data-orientation='horizontal'], /* </DEPRECATED> */
.lm-TabBar[data-orientation='horizontal'] {
  flex-direction: row;
  align-items: flex-end;
}


/* <DEPRECATED> */ .p-TabBar[data-orientation='vertical'], /* </DEPRECATED> */
.lm-TabBar[data-orientation='vertical'] {
  flex-direction: column;
  align-items: flex-end;
}


/* <DEPRECATED> */ .p-TabBar-content, /* </DEPRECATED> */
.lm-TabBar-content {
  margin: 0;
  padding: 0;
  display: flex;
  flex: 1 1 auto;
  list-style-type: none;
}


/* <DEPRECATED> */
.p-TabBar[data-orientation='horizontal'] > .p-TabBar-content,
/* </DEPRECATED> */
.lm-TabBar[data-orientation='horizontal'] > .lm-TabBar-content {
  flex-direction: row;
}


/* <DEPRECATED> */
.p-TabBar[data-orientation='vertical'] > .p-TabBar-content,
/* </DEPRECATED> */
.lm-TabBar[data-orientation='vertical'] > .lm-TabBar-content {
  flex-direction: column;
}


/* <DEPRECATED> */ .p-TabBar-tab, /* </DEPRECATED> */
.lm-TabBar-tab {
  display: flex;
  flex-direction: row;
  box-sizing: border-box;
  overflow: hidden;
}


/* <DEPRECATED> */
.p-TabBar-tabIcon,
.p-TabBar-tabCloseIcon,
/* </DEPRECATED> */
.lm-TabBar-tabIcon,
.lm-TabBar-tabCloseIcon {
  flex: 0 0 auto;
}


/* <DEPRECATED> */ .p-TabBar-tabLabel, /* </DEPRECATED> */
.lm-TabBar-tabLabel {
  flex: 1 1 auto;
  overflow: hidden;
  white-space: nowrap;
}


.lm-TabBar-tabInput {
  user-select: all;
  width: 100%;
  box-sizing : border-box;
}


/* <DEPRECATED> */ .p-TabBar-tab.p-mod-hidden, /* </DEPRECATED> */
.lm-TabBar-tab.lm-mod-hidden {
  display: none !important;
}


.lm-TabBar-addButton.lm-mod-hidden {
  display: none !important;
}


/* <DEPRECATED> */ .p-TabBar.p-mod-dragging .p-TabBar-tab, /* </DEPRECATED> */
.lm-TabBar.lm-mod-dragging .lm-TabBar-tab {
  position: relative;
}


/* <DEPRECATED> */
.p-TabBar.p-mod-dragging[data-orientation='horizontal'] .p-TabBar-tab,
/* </DEPRECATED> */
.lm-TabBar.lm-mod-dragging[data-orientation='horizontal'] .lm-TabBar-tab {
  left: 0;
  transition: left 150ms ease;
}


/* <DEPRECATED> */
.p-TabBar.p-mod-dragging[data-orientation='vertical'] .p-TabBar-tab,
/* </DEPRECATED> */
.lm-TabBar.lm-mod-dragging[data-orientation='vertical'] .lm-TabBar-tab {
  top: 0;
  transition: top 150ms ease;
}


/* <DEPRECATED> */
.p-TabBar.p-mod-dragging .p-TabBar-tab.p-mod-dragging,
/* </DEPRECATED> */
.lm-TabBar.lm-mod-dragging .lm-TabBar-tab.lm-mod-dragging {
  transition: none;
}

.lm-TabBar-tabLabel .lm-TabBar-tabInput {
  user-select: all;
  width: 100%;
  box-sizing : border-box;
  background: inherit;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/


/* <DEPRECATED> */ .p-TabPanel-tabBar, /* </DEPRECATED> */
.lm-TabPanel-tabBar {
  z-index: 1;
}


/* <DEPRECATED> */ .p-TabPanel-stackedPanel, /* </DEPRECATED> */
.lm-TabPanel-stackedPanel {
  z-index: 0;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/

@charset "UTF-8";
html{
  -webkit-box-sizing:border-box;
          box-sizing:border-box; }

*,
*::before,
*::after{
  -webkit-box-sizing:inherit;
          box-sizing:inherit; }

body{
  font-size:14px;
  font-weight:400;
  letter-spacing:0;
  line-height:1.28581;
  text-transform:none;
  color:#182026;
  font-family:-apple-system, "BlinkMacSystemFont", "Segoe UI", "Roboto", "Oxygen", "Ubuntu", "Cantarell", "Open Sans", "Helvetica Neue", "Icons16", sans-serif; }

p{
  margin-bottom:10px;
  margin-top:0; }

small{
  font-size:12px; }

strong{
  font-weight:600; }

::-moz-selection{
  background:rgba(125, 188, 255, 0.6); }

::selection{
  background:rgba(125, 188, 255, 0.6); }
.bp3-heading{
  color:#182026;
  font-weight:600;
  margin:0 0 10px;
  padding:0; }
  .bp3-dark .bp3-heading{
    color:#f5f8fa; }

h1.bp3-heading, .bp3-running-text h1{
  font-size:36px;
  line-height:40px; }

h2.bp3-heading, .bp3-running-text h2{
  font-size:28px;
  line-height:32px; }

h3.bp3-heading, .bp3-running-text h3{
  font-size:22px;
  line-height:25px; }

h4.bp3-heading, .bp3-running-text h4{
  font-size:18px;
  line-height:21px; }

h5.bp3-heading, .bp3-running-text h5{
  font-size:16px;
  line-height:19px; }

h6.bp3-heading, .bp3-running-text h6{
  font-size:14px;
  line-height:16px; }
.bp3-ui-text{
  font-size:14px;
  font-weight:400;
  letter-spacing:0;
  line-height:1.28581;
  text-transform:none; }

.bp3-monospace-text{
  font-family:monospace;
  text-transform:none; }

.bp3-text-muted{
  color:#5c7080; }
  .bp3-dark .bp3-text-muted{
    color:#a7b6c2; }

.bp3-text-disabled{
  color:rgba(92, 112, 128, 0.6); }
  .bp3-dark .bp3-text-disabled{
    color:rgba(167, 182, 194, 0.6); }

.bp3-text-overflow-ellipsis{
  overflow:hidden;
  text-overflow:ellipsis;
  white-space:nowrap;
  word-wrap:normal; }
.bp3-running-text{
  font-size:14px;
  line-height:1.5; }
  .bp3-running-text h1{
    color:#182026;
    font-weight:600;
    margin-bottom:20px;
    margin-top:40px; }
    .bp3-dark .bp3-running-text h1{
      color:#f5f8fa; }
  .bp3-running-text h2{
    color:#182026;
    font-weight:600;
    margin-bottom:20px;
    margin-top:40px; }
    .bp3-dark .bp3-running-text h2{
      color:#f5f8fa; }
  .bp3-running-text h3{
    color:#182026;
    font-weight:600;
    margin-bottom:20px;
    margin-top:40px; }
    .bp3-dark .bp3-running-text h3{
      color:#f5f8fa; }
  .bp3-running-text h4{
    color:#182026;
    font-weight:600;
    margin-bottom:20px;
    margin-top:40px; }
    .bp3-dark .bp3-running-text h4{
      color:#f5f8fa; }
  .bp3-running-text h5{
    color:#182026;
    font-weight:600;
    margin-bottom:20px;
    margin-top:40px; }
    .bp3-dark .bp3-running-text h5{
      color:#f5f8fa; }
  .bp3-running-text h6{
    color:#182026;
    font-weight:600;
    margin-bottom:20px;
    margin-top:40px; }
    .bp3-dark .bp3-running-text h6{
      color:#f5f8fa; }
  .bp3-running-text hr{
    border:none;
    border-bottom:1px solid rgba(16, 22, 26, 0.15);
    margin:20px 0; }
    .bp3-dark .bp3-running-text hr{
      border-color:rgba(255, 255, 255, 0.15); }
  .bp3-running-text p{
    margin:0 0 10px;
    padding:0; }

.bp3-text-large{
  font-size:16px; }

.bp3-text-small{
  font-size:12px; }
a{
  color:#106ba3;
  text-decoration:none; }
  a:hover{
    color:#106ba3;
    cursor:pointer;
    text-decoration:underline; }
  a .bp3-icon, a .bp3-icon-standard, a .bp3-icon-large{
    color:inherit; }
  a code,
  .bp3-dark a code{
    color:inherit; }
  .bp3-dark a,
  .bp3-dark a:hover{
    color:#48aff0; }
    .bp3-dark a .bp3-icon, .bp3-dark a .bp3-icon-standard, .bp3-dark a .bp3-icon-large,
    .bp3-dark a:hover .bp3-icon,
    .bp3-dark a:hover .bp3-icon-standard,
    .bp3-dark a:hover .bp3-icon-large{
      color:inherit; }
.bp3-running-text code, .bp3-code{
  font-family:monospace;
  text-transform:none;
  background:rgba(255, 255, 255, 0.7);
  border-radius:3px;
  -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2);
          box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2);
  color:#5c7080;
  font-size:smaller;
  padding:2px 5px; }
  .bp3-dark .bp3-running-text code, .bp3-running-text .bp3-dark code, .bp3-dark .bp3-code{
    background:rgba(16, 22, 26, 0.3);
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4);
    color:#a7b6c2; }
  .bp3-running-text a > code, a > .bp3-code{
    color:#137cbd; }
    .bp3-dark .bp3-running-text a > code, .bp3-running-text .bp3-dark a > code, .bp3-dark a > .bp3-code{
      color:inherit; }

.bp3-running-text pre, .bp3-code-block{
  font-family:monospace;
  text-transform:none;
  background:rgba(255, 255, 255, 0.7);
  border-radius:3px;
  -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.15);
          box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.15);
  color:#182026;
  display:block;
  font-size:13px;
  line-height:1.4;
  margin:10px 0;
  padding:13px 15px 12px;
  word-break:break-all;
  word-wrap:break-word; }
  .bp3-dark .bp3-running-text pre, .bp3-running-text .bp3-dark pre, .bp3-dark .bp3-code-block{
    background:rgba(16, 22, 26, 0.3);
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4);
    color:#f5f8fa; }
  .bp3-running-text pre > code, .bp3-code-block > code{
    background:none;
    -webkit-box-shadow:none;
            box-shadow:none;
    color:inherit;
    font-size:inherit;
    padding:0; }

.bp3-running-text kbd, .bp3-key{
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center;
  background:#ffffff;
  border-radius:3px;
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.2);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.2);
  color:#5c7080;
  display:-webkit-inline-box;
  display:-ms-inline-flexbox;
  display:inline-flex;
  font-family:inherit;
  font-size:12px;
  height:24px;
  -webkit-box-pack:center;
      -ms-flex-pack:center;
          justify-content:center;
  line-height:24px;
  min-width:24px;
  padding:3px 6px;
  vertical-align:middle; }
  .bp3-running-text kbd .bp3-icon, .bp3-key .bp3-icon, .bp3-running-text kbd .bp3-icon-standard, .bp3-key .bp3-icon-standard, .bp3-running-text kbd .bp3-icon-large, .bp3-key .bp3-icon-large{
    margin-right:5px; }
  .bp3-dark .bp3-running-text kbd, .bp3-running-text .bp3-dark kbd, .bp3-dark .bp3-key{
    background:#394b59;
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.4);
    color:#a7b6c2; }
.bp3-running-text blockquote, .bp3-blockquote{
  border-left:solid 4px rgba(167, 182, 194, 0.5);
  margin:0 0 10px;
  padding:0 20px; }
  .bp3-dark .bp3-running-text blockquote, .bp3-running-text .bp3-dark blockquote, .bp3-dark .bp3-blockquote{
    border-color:rgba(115, 134, 148, 0.5); }
.bp3-running-text ul,
.bp3-running-text ol, .bp3-list{
  margin:10px 0;
  padding-left:30px; }
  .bp3-running-text ul li:not(:last-child), .bp3-running-text ol li:not(:last-child), .bp3-list li:not(:last-child){
    margin-bottom:5px; }
  .bp3-running-text ul ol, .bp3-running-text ol ol, .bp3-list ol,
  .bp3-running-text ul ul,
  .bp3-running-text ol ul,
  .bp3-list ul{
    margin-top:5px; }

.bp3-list-unstyled{
  list-style:none;
  margin:0;
  padding:0; }
  .bp3-list-unstyled li{
    padding:0; }
.bp3-rtl{
  text-align:right; }

.bp3-dark{
  color:#f5f8fa; }

:focus{
  outline:rgba(19, 124, 189, 0.6) auto 2px;
  outline-offset:2px;
  -moz-outline-radius:6px; }

.bp3-focus-disabled :focus{
  outline:none !important; }
  .bp3-focus-disabled :focus ~ .bp3-control-indicator{
    outline:none !important; }

.bp3-alert{
  max-width:400px;
  padding:20px; }

.bp3-alert-body{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex; }
  .bp3-alert-body .bp3-icon{
    font-size:40px;
    margin-right:20px;
    margin-top:0; }

.bp3-alert-contents{
  word-break:break-word; }

.bp3-alert-footer{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-orient:horizontal;
  -webkit-box-direction:reverse;
      -ms-flex-direction:row-reverse;
          flex-direction:row-reverse;
  margin-top:10px; }
  .bp3-alert-footer .bp3-button{
    margin-left:10px; }
.bp3-breadcrumbs{
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center;
  cursor:default;
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -ms-flex-wrap:wrap;
      flex-wrap:wrap;
  height:30px;
  list-style:none;
  margin:0;
  padding:0; }
  .bp3-breadcrumbs > li{
    -webkit-box-align:center;
        -ms-flex-align:center;
            align-items:center;
    display:-webkit-box;
    display:-ms-flexbox;
    display:flex; }
    .bp3-breadcrumbs > li::after{
      background:url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 16 16'%3e%3cpath fill-rule='evenodd' clip-rule='evenodd' d='M10.71 7.29l-4-4a1.003 1.003 0 00-1.42 1.42L8.59 8 5.3 11.29c-.19.18-.3.43-.3.71a1.003 1.003 0 001.71.71l4-4c.18-.18.29-.43.29-.71 0-.28-.11-.53-.29-.71z' fill='%235C7080'/%3e%3c/svg%3e");
      content:"";
      display:block;
      height:16px;
      margin:0 5px;
      width:16px; }
    .bp3-breadcrumbs > li:last-of-type::after{
      display:none; }

.bp3-breadcrumb,
.bp3-breadcrumb-current,
.bp3-breadcrumbs-collapsed{
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center;
  display:-webkit-inline-box;
  display:-ms-inline-flexbox;
  display:inline-flex;
  font-size:16px; }

.bp3-breadcrumb,
.bp3-breadcrumbs-collapsed{
  color:#5c7080; }

.bp3-breadcrumb:hover{
  text-decoration:none; }

.bp3-breadcrumb.bp3-disabled{
  color:rgba(92, 112, 128, 0.6);
  cursor:not-allowed; }

.bp3-breadcrumb .bp3-icon{
  margin-right:5px; }

.bp3-breadcrumb-current{
  color:inherit;
  font-weight:600; }
  .bp3-breadcrumb-current .bp3-input{
    font-size:inherit;
    font-weight:inherit;
    vertical-align:baseline; }

.bp3-breadcrumbs-collapsed{
  background:#ced9e0;
  border:none;
  border-radius:3px;
  cursor:pointer;
  margin-right:2px;
  padding:1px 5px;
  vertical-align:text-bottom; }
  .bp3-breadcrumbs-collapsed::before{
    background:url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 16 16'%3e%3cg fill='%235C7080'%3e%3ccircle cx='2' cy='8.03' r='2'/%3e%3ccircle cx='14' cy='8.03' r='2'/%3e%3ccircle cx='8' cy='8.03' r='2'/%3e%3c/g%3e%3c/svg%3e") center no-repeat;
    content:"";
    display:block;
    height:16px;
    width:16px; }
  .bp3-breadcrumbs-collapsed:hover{
    background:#bfccd6;
    color:#182026;
    text-decoration:none; }

.bp3-dark .bp3-breadcrumb,
.bp3-dark .bp3-breadcrumbs-collapsed{
  color:#a7b6c2; }

.bp3-dark .bp3-breadcrumbs > li::after{
  color:#a7b6c2; }

.bp3-dark .bp3-breadcrumb.bp3-disabled{
  color:rgba(167, 182, 194, 0.6); }

.bp3-dark .bp3-breadcrumb-current{
  color:#f5f8fa; }

.bp3-dark .bp3-breadcrumbs-collapsed{
  background:rgba(16, 22, 26, 0.4); }
  .bp3-dark .bp3-breadcrumbs-collapsed:hover{
    background:rgba(16, 22, 26, 0.6);
    color:#f5f8fa; }
.bp3-button{
  display:-webkit-inline-box;
  display:-ms-inline-flexbox;
  display:inline-flex;
  -webkit-box-orient:horizontal;
  -webkit-box-direction:normal;
      -ms-flex-direction:row;
          flex-direction:row;
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center;
  border:none;
  border-radius:3px;
  cursor:pointer;
  font-size:14px;
  -webkit-box-pack:center;
      -ms-flex-pack:center;
          justify-content:center;
  padding:5px 10px;
  text-align:left;
  vertical-align:middle;
  min-height:30px;
  min-width:30px; }
  .bp3-button > *{
    -webkit-box-flex:0;
        -ms-flex-positive:0;
            flex-grow:0;
    -ms-flex-negative:0;
        flex-shrink:0; }
  .bp3-button > .bp3-fill{
    -webkit-box-flex:1;
        -ms-flex-positive:1;
            flex-grow:1;
    -ms-flex-negative:1;
        flex-shrink:1; }
  .bp3-button::before,
  .bp3-button > *{
    margin-right:7px; }
  .bp3-button:empty::before,
  .bp3-button > :last-child{
    margin-right:0; }
  .bp3-button:empty{
    padding:0 !important; }
  .bp3-button:disabled, .bp3-button.bp3-disabled{
    cursor:not-allowed; }
  .bp3-button.bp3-fill{
    display:-webkit-box;
    display:-ms-flexbox;
    display:flex;
    width:100%; }
  .bp3-button.bp3-align-right,
  .bp3-align-right .bp3-button{
    text-align:right; }
  .bp3-button.bp3-align-left,
  .bp3-align-left .bp3-button{
    text-align:left; }
  .bp3-button:not([class*="bp3-intent-"]){
    background-color:#f5f8fa;
    background-image:-webkit-gradient(linear, left top, left bottom, from(rgba(255, 255, 255, 0.8)), to(rgba(255, 255, 255, 0)));
    background-image:linear-gradient(to bottom, rgba(255, 255, 255, 0.8), rgba(255, 255, 255, 0));
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
    color:#182026; }
    .bp3-button:not([class*="bp3-intent-"]):hover{
      background-clip:padding-box;
      background-color:#ebf1f5;
      -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
              box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1); }
    .bp3-button:not([class*="bp3-intent-"]):active, .bp3-button:not([class*="bp3-intent-"]).bp3-active{
      background-color:#d8e1e8;
      background-image:none;
      -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 1px 2px rgba(16, 22, 26, 0.2);
              box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 1px 2px rgba(16, 22, 26, 0.2); }
    .bp3-button:not([class*="bp3-intent-"]):disabled, .bp3-button:not([class*="bp3-intent-"]).bp3-disabled{
      background-color:rgba(206, 217, 224, 0.5);
      background-image:none;
      -webkit-box-shadow:none;
              box-shadow:none;
      color:rgba(92, 112, 128, 0.6);
      cursor:not-allowed;
      outline:none; }
      .bp3-button:not([class*="bp3-intent-"]):disabled.bp3-active, .bp3-button:not([class*="bp3-intent-"]):disabled.bp3-active:hover, .bp3-button:not([class*="bp3-intent-"]).bp3-disabled.bp3-active, .bp3-button:not([class*="bp3-intent-"]).bp3-disabled.bp3-active:hover{
        background:rgba(206, 217, 224, 0.7); }
  .bp3-button.bp3-intent-primary{
    background-color:#137cbd;
    background-image:-webkit-gradient(linear, left top, left bottom, from(rgba(255, 255, 255, 0.1)), to(rgba(255, 255, 255, 0)));
    background-image:linear-gradient(to bottom, rgba(255, 255, 255, 0.1), rgba(255, 255, 255, 0));
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
    color:#ffffff; }
    .bp3-button.bp3-intent-primary:hover, .bp3-button.bp3-intent-primary:active, .bp3-button.bp3-intent-primary.bp3-active{
      color:#ffffff; }
    .bp3-button.bp3-intent-primary:hover{
      background-color:#106ba3;
      -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
              box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2); }
    .bp3-button.bp3-intent-primary:active, .bp3-button.bp3-intent-primary.bp3-active{
      background-color:#0e5a8a;
      background-image:none;
      -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2);
              box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2); }
    .bp3-button.bp3-intent-primary:disabled, .bp3-button.bp3-intent-primary.bp3-disabled{
      background-color:rgba(19, 124, 189, 0.5);
      background-image:none;
      border-color:transparent;
      -webkit-box-shadow:none;
              box-shadow:none;
      color:rgba(255, 255, 255, 0.6); }
  .bp3-button.bp3-intent-success{
    background-color:#0f9960;
    background-image:-webkit-gradient(linear, left top, left bottom, from(rgba(255, 255, 255, 0.1)), to(rgba(255, 255, 255, 0)));
    background-image:linear-gradient(to bottom, rgba(255, 255, 255, 0.1), rgba(255, 255, 255, 0));
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
    color:#ffffff; }
    .bp3-button.bp3-intent-success:hover, .bp3-button.bp3-intent-success:active, .bp3-button.bp3-intent-success.bp3-active{
      color:#ffffff; }
    .bp3-button.bp3-intent-success:hover{
      background-color:#0d8050;
      -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
              box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2); }
    .bp3-button.bp3-intent-success:active, .bp3-button.bp3-intent-success.bp3-active{
      background-color:#0a6640;
      background-image:none;
      -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2);
              box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2); }
    .bp3-button.bp3-intent-success:disabled, .bp3-button.bp3-intent-success.bp3-disabled{
      background-color:rgba(15, 153, 96, 0.5);
      background-image:none;
      border-color:transparent;
      -webkit-box-shadow:none;
              box-shadow:none;
      color:rgba(255, 255, 255, 0.6); }
  .bp3-button.bp3-intent-warning{
    background-color:#d9822b;
    background-image:-webkit-gradient(linear, left top, left bottom, from(rgba(255, 255, 255, 0.1)), to(rgba(255, 255, 255, 0)));
    background-image:linear-gradient(to bottom, rgba(255, 255, 255, 0.1), rgba(255, 255, 255, 0));
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
    color:#ffffff; }
    .bp3-button.bp3-intent-warning:hover, .bp3-button.bp3-intent-warning:active, .bp3-button.bp3-intent-warning.bp3-active{
      color:#ffffff; }
    .bp3-button.bp3-intent-warning:hover{
      background-color:#bf7326;
      -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
              box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2); }
    .bp3-button.bp3-intent-warning:active, .bp3-button.bp3-intent-warning.bp3-active{
      background-color:#a66321;
      background-image:none;
      -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2);
              box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2); }
    .bp3-button.bp3-intent-warning:disabled, .bp3-button.bp3-intent-warning.bp3-disabled{
      background-color:rgba(217, 130, 43, 0.5);
      background-image:none;
      border-color:transparent;
      -webkit-box-shadow:none;
              box-shadow:none;
      color:rgba(255, 255, 255, 0.6); }
  .bp3-button.bp3-intent-danger{
    background-color:#db3737;
    background-image:-webkit-gradient(linear, left top, left bottom, from(rgba(255, 255, 255, 0.1)), to(rgba(255, 255, 255, 0)));
    background-image:linear-gradient(to bottom, rgba(255, 255, 255, 0.1), rgba(255, 255, 255, 0));
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
    color:#ffffff; }
    .bp3-button.bp3-intent-danger:hover, .bp3-button.bp3-intent-danger:active, .bp3-button.bp3-intent-danger.bp3-active{
      color:#ffffff; }
    .bp3-button.bp3-intent-danger:hover{
      background-color:#c23030;
      -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
              box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2); }
    .bp3-button.bp3-intent-danger:active, .bp3-button.bp3-intent-danger.bp3-active{
      background-color:#a82a2a;
      background-image:none;
      -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2);
              box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2); }
    .bp3-button.bp3-intent-danger:disabled, .bp3-button.bp3-intent-danger.bp3-disabled{
      background-color:rgba(219, 55, 55, 0.5);
      background-image:none;
      border-color:transparent;
      -webkit-box-shadow:none;
              box-shadow:none;
      color:rgba(255, 255, 255, 0.6); }
  .bp3-button[class*="bp3-intent-"] .bp3-button-spinner .bp3-spinner-head{
    stroke:#ffffff; }
  .bp3-button.bp3-large,
  .bp3-large .bp3-button{
    min-height:40px;
    min-width:40px;
    font-size:16px;
    padding:5px 15px; }
    .bp3-button.bp3-large::before,
    .bp3-button.bp3-large > *,
    .bp3-large .bp3-button::before,
    .bp3-large .bp3-button > *{
      margin-right:10px; }
    .bp3-button.bp3-large:empty::before,
    .bp3-button.bp3-large > :last-child,
    .bp3-large .bp3-button:empty::before,
    .bp3-large .bp3-button > :last-child{
      margin-right:0; }
  .bp3-button.bp3-small,
  .bp3-small .bp3-button{
    min-height:24px;
    min-width:24px;
    padding:0 7px; }
  .bp3-button.bp3-loading{
    position:relative; }
    .bp3-button.bp3-loading[class*="bp3-icon-"]::before{
      visibility:hidden; }
    .bp3-button.bp3-loading .bp3-button-spinner{
      margin:0;
      position:absolute; }
    .bp3-button.bp3-loading > :not(.bp3-button-spinner){
      visibility:hidden; }
  .bp3-button[class*="bp3-icon-"]::before{
    font-family:"Icons16", sans-serif;
    font-size:16px;
    font-style:normal;
    font-weight:400;
    line-height:1;
    -moz-osx-font-smoothing:grayscale;
    -webkit-font-smoothing:antialiased;
    color:#5c7080; }
  .bp3-button .bp3-icon, .bp3-button .bp3-icon-standard, .bp3-button .bp3-icon-large{
    color:#5c7080; }
    .bp3-button .bp3-icon.bp3-align-right, .bp3-button .bp3-icon-standard.bp3-align-right, .bp3-button .bp3-icon-large.bp3-align-right{
      margin-left:7px; }
  .bp3-button .bp3-icon:first-child:last-child,
  .bp3-button .bp3-spinner + .bp3-icon:last-child{
    margin:0 -7px; }
  .bp3-dark .bp3-button:not([class*="bp3-intent-"]){
    background-color:#394b59;
    background-image:-webkit-gradient(linear, left top, left bottom, from(rgba(255, 255, 255, 0.05)), to(rgba(255, 255, 255, 0)));
    background-image:linear-gradient(to bottom, rgba(255, 255, 255, 0.05), rgba(255, 255, 255, 0));
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
    color:#f5f8fa; }
    .bp3-dark .bp3-button:not([class*="bp3-intent-"]):hover, .bp3-dark .bp3-button:not([class*="bp3-intent-"]):active, .bp3-dark .bp3-button:not([class*="bp3-intent-"]).bp3-active{
      color:#f5f8fa; }
    .bp3-dark .bp3-button:not([class*="bp3-intent-"]):hover{
      background-color:#30404d;
      -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4); }
    .bp3-dark .bp3-button:not([class*="bp3-intent-"]):active, .bp3-dark .bp3-button:not([class*="bp3-intent-"]).bp3-active{
      background-color:#202b33;
      background-image:none;
      -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.6), inset 0 1px 2px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px rgba(16, 22, 26, 0.6), inset 0 1px 2px rgba(16, 22, 26, 0.2); }
    .bp3-dark .bp3-button:not([class*="bp3-intent-"]):disabled, .bp3-dark .bp3-button:not([class*="bp3-intent-"]).bp3-disabled{
      background-color:rgba(57, 75, 89, 0.5);
      background-image:none;
      -webkit-box-shadow:none;
              box-shadow:none;
      color:rgba(167, 182, 194, 0.6); }
      .bp3-dark .bp3-button:not([class*="bp3-intent-"]):disabled.bp3-active, .bp3-dark .bp3-button:not([class*="bp3-intent-"]).bp3-disabled.bp3-active{
        background:rgba(57, 75, 89, 0.7); }
    .bp3-dark .bp3-button:not([class*="bp3-intent-"]) .bp3-button-spinner .bp3-spinner-head{
      background:rgba(16, 22, 26, 0.5);
      stroke:#8a9ba8; }
    .bp3-dark .bp3-button:not([class*="bp3-intent-"])[class*="bp3-icon-"]::before{
      color:#a7b6c2; }
    .bp3-dark .bp3-button:not([class*="bp3-intent-"]) .bp3-icon, .bp3-dark .bp3-button:not([class*="bp3-intent-"]) .bp3-icon-standard, .bp3-dark .bp3-button:not([class*="bp3-intent-"]) .bp3-icon-large{
      color:#a7b6c2; }
  .bp3-dark .bp3-button[class*="bp3-intent-"]{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4); }
    .bp3-dark .bp3-button[class*="bp3-intent-"]:hover{
      -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4); }
    .bp3-dark .bp3-button[class*="bp3-intent-"]:active, .bp3-dark .bp3-button[class*="bp3-intent-"].bp3-active{
      -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2); }
    .bp3-dark .bp3-button[class*="bp3-intent-"]:disabled, .bp3-dark .bp3-button[class*="bp3-intent-"].bp3-disabled{
      background-image:none;
      -webkit-box-shadow:none;
              box-shadow:none;
      color:rgba(255, 255, 255, 0.3); }
    .bp3-dark .bp3-button[class*="bp3-intent-"] .bp3-button-spinner .bp3-spinner-head{
      stroke:#8a9ba8; }
  .bp3-button:disabled::before,
  .bp3-button:disabled .bp3-icon, .bp3-button:disabled .bp3-icon-standard, .bp3-button:disabled .bp3-icon-large, .bp3-button.bp3-disabled::before,
  .bp3-button.bp3-disabled .bp3-icon, .bp3-button.bp3-disabled .bp3-icon-standard, .bp3-button.bp3-disabled .bp3-icon-large, .bp3-button[class*="bp3-intent-"]::before,
  .bp3-button[class*="bp3-intent-"] .bp3-icon, .bp3-button[class*="bp3-intent-"] .bp3-icon-standard, .bp3-button[class*="bp3-intent-"] .bp3-icon-large{
    color:inherit !important; }
  .bp3-button.bp3-minimal{
    background:none;
    -webkit-box-shadow:none;
            box-shadow:none; }
    .bp3-button.bp3-minimal:hover{
      background:rgba(167, 182, 194, 0.3);
      -webkit-box-shadow:none;
              box-shadow:none;
      color:#182026;
      text-decoration:none; }
    .bp3-button.bp3-minimal:active, .bp3-button.bp3-minimal.bp3-active{
      background:rgba(115, 134, 148, 0.3);
      -webkit-box-shadow:none;
              box-shadow:none;
      color:#182026; }
    .bp3-button.bp3-minimal:disabled, .bp3-button.bp3-minimal:disabled:hover, .bp3-button.bp3-minimal.bp3-disabled, .bp3-button.bp3-minimal.bp3-disabled:hover{
      background:none;
      color:rgba(92, 112, 128, 0.6);
      cursor:not-allowed; }
      .bp3-button.bp3-minimal:disabled.bp3-active, .bp3-button.bp3-minimal:disabled:hover.bp3-active, .bp3-button.bp3-minimal.bp3-disabled.bp3-active, .bp3-button.bp3-minimal.bp3-disabled:hover.bp3-active{
        background:rgba(115, 134, 148, 0.3); }
    .bp3-dark .bp3-button.bp3-minimal{
      background:none;
      -webkit-box-shadow:none;
              box-shadow:none;
      color:inherit; }
      .bp3-dark .bp3-button.bp3-minimal:hover, .bp3-dark .bp3-button.bp3-minimal:active, .bp3-dark .bp3-button.bp3-minimal.bp3-active{
        background:none;
        -webkit-box-shadow:none;
                box-shadow:none; }
      .bp3-dark .bp3-button.bp3-minimal:hover{
        background:rgba(138, 155, 168, 0.15); }
      .bp3-dark .bp3-button.bp3-minimal:active, .bp3-dark .bp3-button.bp3-minimal.bp3-active{
        background:rgba(138, 155, 168, 0.3);
        color:#f5f8fa; }
      .bp3-dark .bp3-button.bp3-minimal:disabled, .bp3-dark .bp3-button.bp3-minimal:disabled:hover, .bp3-dark .bp3-button.bp3-minimal.bp3-disabled, .bp3-dark .bp3-button.bp3-minimal.bp3-disabled:hover{
        background:none;
        color:rgba(167, 182, 194, 0.6);
        cursor:not-allowed; }
        .bp3-dark .bp3-button.bp3-minimal:disabled.bp3-active, .bp3-dark .bp3-button.bp3-minimal:disabled:hover.bp3-active, .bp3-dark .bp3-button.bp3-minimal.bp3-disabled.bp3-active, .bp3-dark .bp3-button.bp3-minimal.bp3-disabled:hover.bp3-active{
          background:rgba(138, 155, 168, 0.3); }
    .bp3-button.bp3-minimal.bp3-intent-primary{
      color:#106ba3; }
      .bp3-button.bp3-minimal.bp3-intent-primary:hover, .bp3-button.bp3-minimal.bp3-intent-primary:active, .bp3-button.bp3-minimal.bp3-intent-primary.bp3-active{
        background:none;
        -webkit-box-shadow:none;
                box-shadow:none;
        color:#106ba3; }
      .bp3-button.bp3-minimal.bp3-intent-primary:hover{
        background:rgba(19, 124, 189, 0.15);
        color:#106ba3; }
      .bp3-button.bp3-minimal.bp3-intent-primary:active, .bp3-button.bp3-minimal.bp3-intent-primary.bp3-active{
        background:rgba(19, 124, 189, 0.3);
        color:#106ba3; }
      .bp3-button.bp3-minimal.bp3-intent-primary:disabled, .bp3-button.bp3-minimal.bp3-intent-primary.bp3-disabled{
        background:none;
        color:rgba(16, 107, 163, 0.5); }
        .bp3-button.bp3-minimal.bp3-intent-primary:disabled.bp3-active, .bp3-button.bp3-minimal.bp3-intent-primary.bp3-disabled.bp3-active{
          background:rgba(19, 124, 189, 0.3); }
      .bp3-button.bp3-minimal.bp3-intent-primary .bp3-button-spinner .bp3-spinner-head{
        stroke:#106ba3; }
      .bp3-dark .bp3-button.bp3-minimal.bp3-intent-primary{
        color:#48aff0; }
        .bp3-dark .bp3-button.bp3-minimal.bp3-intent-primary:hover{
          background:rgba(19, 124, 189, 0.2);
          color:#48aff0; }
        .bp3-dark .bp3-button.bp3-minimal.bp3-intent-primary:active, .bp3-dark .bp3-button.bp3-minimal.bp3-intent-primary.bp3-active{
          background:rgba(19, 124, 189, 0.3);
          color:#48aff0; }
        .bp3-dark .bp3-button.bp3-minimal.bp3-intent-primary:disabled, .bp3-dark .bp3-button.bp3-minimal.bp3-intent-primary.bp3-disabled{
          background:none;
          color:rgba(72, 175, 240, 0.5); }
          .bp3-dark .bp3-button.bp3-minimal.bp3-intent-primary:disabled.bp3-active, .bp3-dark .bp3-button.bp3-minimal.bp3-intent-primary.bp3-disabled.bp3-active{
            background:rgba(19, 124, 189, 0.3); }
    .bp3-button.bp3-minimal.bp3-intent-success{
      color:#0d8050; }
      .bp3-button.bp3-minimal.bp3-intent-success:hover, .bp3-button.bp3-minimal.bp3-intent-success:active, .bp3-button.bp3-minimal.bp3-intent-success.bp3-active{
        background:none;
        -webkit-box-shadow:none;
                box-shadow:none;
        color:#0d8050; }
      .bp3-button.bp3-minimal.bp3-intent-success:hover{
        background:rgba(15, 153, 96, 0.15);
        color:#0d8050; }
      .bp3-button.bp3-minimal.bp3-intent-success:active, .bp3-button.bp3-minimal.bp3-intent-success.bp3-active{
        background:rgba(15, 153, 96, 0.3);
        color:#0d8050; }
      .bp3-button.bp3-minimal.bp3-intent-success:disabled, .bp3-button.bp3-minimal.bp3-intent-success.bp3-disabled{
        background:none;
        color:rgba(13, 128, 80, 0.5); }
        .bp3-button.bp3-minimal.bp3-intent-success:disabled.bp3-active, .bp3-button.bp3-minimal.bp3-intent-success.bp3-disabled.bp3-active{
          background:rgba(15, 153, 96, 0.3); }
      .bp3-button.bp3-minimal.bp3-intent-success .bp3-button-spinner .bp3-spinner-head{
        stroke:#0d8050; }
      .bp3-dark .bp3-button.bp3-minimal.bp3-intent-success{
        color:#3dcc91; }
        .bp3-dark .bp3-button.bp3-minimal.bp3-intent-success:hover{
          background:rgba(15, 153, 96, 0.2);
          color:#3dcc91; }
        .bp3-dark .bp3-button.bp3-minimal.bp3-intent-success:active, .bp3-dark .bp3-button.bp3-minimal.bp3-intent-success.bp3-active{
          background:rgba(15, 153, 96, 0.3);
          color:#3dcc91; }
        .bp3-dark .bp3-button.bp3-minimal.bp3-intent-success:disabled, .bp3-dark .bp3-button.bp3-minimal.bp3-intent-success.bp3-disabled{
          background:none;
          color:rgba(61, 204, 145, 0.5); }
          .bp3-dark .bp3-button.bp3-minimal.bp3-intent-success:disabled.bp3-active, .bp3-dark .bp3-button.bp3-minimal.bp3-intent-success.bp3-disabled.bp3-active{
            background:rgba(15, 153, 96, 0.3); }
    .bp3-button.bp3-minimal.bp3-intent-warning{
      color:#bf7326; }
      .bp3-button.bp3-minimal.bp3-intent-warning:hover, .bp3-button.bp3-minimal.bp3-intent-warning:active, .bp3-button.bp3-minimal.bp3-intent-warning.bp3-active{
        background:none;
        -webkit-box-shadow:none;
                box-shadow:none;
        color:#bf7326; }
      .bp3-button.bp3-minimal.bp3-intent-warning:hover{
        background:rgba(217, 130, 43, 0.15);
        color:#bf7326; }
      .bp3-button.bp3-minimal.bp3-intent-warning:active, .bp3-button.bp3-minimal.bp3-intent-warning.bp3-active{
        background:rgba(217, 130, 43, 0.3);
        color:#bf7326; }
      .bp3-button.bp3-minimal.bp3-intent-warning:disabled, .bp3-button.bp3-minimal.bp3-intent-warning.bp3-disabled{
        background:none;
        color:rgba(191, 115, 38, 0.5); }
        .bp3-button.bp3-minimal.bp3-intent-warning:disabled.bp3-active, .bp3-button.bp3-minimal.bp3-intent-warning.bp3-disabled.bp3-active{
          background:rgba(217, 130, 43, 0.3); }
      .bp3-button.bp3-minimal.bp3-intent-warning .bp3-button-spinner .bp3-spinner-head{
        stroke:#bf7326; }
      .bp3-dark .bp3-button.bp3-minimal.bp3-intent-warning{
        color:#ffb366; }
        .bp3-dark .bp3-button.bp3-minimal.bp3-intent-warning:hover{
          background:rgba(217, 130, 43, 0.2);
          color:#ffb366; }
        .bp3-dark .bp3-button.bp3-minimal.bp3-intent-warning:active, .bp3-dark .bp3-button.bp3-minimal.bp3-intent-warning.bp3-active{
          background:rgba(217, 130, 43, 0.3);
          color:#ffb366; }
        .bp3-dark .bp3-button.bp3-minimal.bp3-intent-warning:disabled, .bp3-dark .bp3-button.bp3-minimal.bp3-intent-warning.bp3-disabled{
          background:none;
          color:rgba(255, 179, 102, 0.5); }
          .bp3-dark .bp3-button.bp3-minimal.bp3-intent-warning:disabled.bp3-active, .bp3-dark .bp3-button.bp3-minimal.bp3-intent-warning.bp3-disabled.bp3-active{
            background:rgba(217, 130, 43, 0.3); }
    .bp3-button.bp3-minimal.bp3-intent-danger{
      color:#c23030; }
      .bp3-button.bp3-minimal.bp3-intent-danger:hover, .bp3-button.bp3-minimal.bp3-intent-danger:active, .bp3-button.bp3-minimal.bp3-intent-danger.bp3-active{
        background:none;
        -webkit-box-shadow:none;
                box-shadow:none;
        color:#c23030; }
      .bp3-button.bp3-minimal.bp3-intent-danger:hover{
        background:rgba(219, 55, 55, 0.15);
        color:#c23030; }
      .bp3-button.bp3-minimal.bp3-intent-danger:active, .bp3-button.bp3-minimal.bp3-intent-danger.bp3-active{
        background:rgba(219, 55, 55, 0.3);
        color:#c23030; }
      .bp3-button.bp3-minimal.bp3-intent-danger:disabled, .bp3-button.bp3-minimal.bp3-intent-danger.bp3-disabled{
        background:none;
        color:rgba(194, 48, 48, 0.5); }
        .bp3-button.bp3-minimal.bp3-intent-danger:disabled.bp3-active, .bp3-button.bp3-minimal.bp3-intent-danger.bp3-disabled.bp3-active{
          background:rgba(219, 55, 55, 0.3); }
      .bp3-button.bp3-minimal.bp3-intent-danger .bp3-button-spinner .bp3-spinner-head{
        stroke:#c23030; }
      .bp3-dark .bp3-button.bp3-minimal.bp3-intent-danger{
        color:#ff7373; }
        .bp3-dark .bp3-button.bp3-minimal.bp3-intent-danger:hover{
          background:rgba(219, 55, 55, 0.2);
          color:#ff7373; }
        .bp3-dark .bp3-button.bp3-minimal.bp3-intent-danger:active, .bp3-dark .bp3-button.bp3-minimal.bp3-intent-danger.bp3-active{
          background:rgba(219, 55, 55, 0.3);
          color:#ff7373; }
        .bp3-dark .bp3-button.bp3-minimal.bp3-intent-danger:disabled, .bp3-dark .bp3-button.bp3-minimal.bp3-intent-danger.bp3-disabled{
          background:none;
          color:rgba(255, 115, 115, 0.5); }
          .bp3-dark .bp3-button.bp3-minimal.bp3-intent-danger:disabled.bp3-active, .bp3-dark .bp3-button.bp3-minimal.bp3-intent-danger.bp3-disabled.bp3-active{
            background:rgba(219, 55, 55, 0.3); }
  .bp3-button.bp3-outlined{
    background:none;
    -webkit-box-shadow:none;
            box-shadow:none;
    border:1px solid rgba(24, 32, 38, 0.2);
    -webkit-box-sizing:border-box;
            box-sizing:border-box; }
    .bp3-button.bp3-outlined:hover{
      background:rgba(167, 182, 194, 0.3);
      -webkit-box-shadow:none;
              box-shadow:none;
      color:#182026;
      text-decoration:none; }
    .bp3-button.bp3-outlined:active, .bp3-button.bp3-outlined.bp3-active{
      background:rgba(115, 134, 148, 0.3);
      -webkit-box-shadow:none;
              box-shadow:none;
      color:#182026; }
    .bp3-button.bp3-outlined:disabled, .bp3-button.bp3-outlined:disabled:hover, .bp3-button.bp3-outlined.bp3-disabled, .bp3-button.bp3-outlined.bp3-disabled:hover{
      background:none;
      color:rgba(92, 112, 128, 0.6);
      cursor:not-allowed; }
      .bp3-button.bp3-outlined:disabled.bp3-active, .bp3-button.bp3-outlined:disabled:hover.bp3-active, .bp3-button.bp3-outlined.bp3-disabled.bp3-active, .bp3-button.bp3-outlined.bp3-disabled:hover.bp3-active{
        background:rgba(115, 134, 148, 0.3); }
    .bp3-dark .bp3-button.bp3-outlined{
      background:none;
      -webkit-box-shadow:none;
              box-shadow:none;
      color:inherit; }
      .bp3-dark .bp3-button.bp3-outlined:hover, .bp3-dark .bp3-button.bp3-outlined:active, .bp3-dark .bp3-button.bp3-outlined.bp3-active{
        background:none;
        -webkit-box-shadow:none;
                box-shadow:none; }
      .bp3-dark .bp3-button.bp3-outlined:hover{
        background:rgba(138, 155, 168, 0.15); }
      .bp3-dark .bp3-button.bp3-outlined:active, .bp3-dark .bp3-button.bp3-outlined.bp3-active{
        background:rgba(138, 155, 168, 0.3);
        color:#f5f8fa; }
      .bp3-dark .bp3-button.bp3-outlined:disabled, .bp3-dark .bp3-button.bp3-outlined:disabled:hover, .bp3-dark .bp3-button.bp3-outlined.bp3-disabled, .bp3-dark .bp3-button.bp3-outlined.bp3-disabled:hover{
        background:none;
        color:rgba(167, 182, 194, 0.6);
        cursor:not-allowed; }
        .bp3-dark .bp3-button.bp3-outlined:disabled.bp3-active, .bp3-dark .bp3-button.bp3-outlined:disabled:hover.bp3-active, .bp3-dark .bp3-button.bp3-outlined.bp3-disabled.bp3-active, .bp3-dark .bp3-button.bp3-outlined.bp3-disabled:hover.bp3-active{
          background:rgba(138, 155, 168, 0.3); }
    .bp3-button.bp3-outlined.bp3-intent-primary{
      color:#106ba3; }
      .bp3-button.bp3-outlined.bp3-intent-primary:hover, .bp3-button.bp3-outlined.bp3-intent-primary:active, .bp3-button.bp3-outlined.bp3-intent-primary.bp3-active{
        background:none;
        -webkit-box-shadow:none;
                box-shadow:none;
        color:#106ba3; }
      .bp3-button.bp3-outlined.bp3-intent-primary:hover{
        background:rgba(19, 124, 189, 0.15);
        color:#106ba3; }
      .bp3-button.bp3-outlined.bp3-intent-primary:active, .bp3-button.bp3-outlined.bp3-intent-primary.bp3-active{
        background:rgba(19, 124, 189, 0.3);
        color:#106ba3; }
      .bp3-button.bp3-outlined.bp3-intent-primary:disabled, .bp3-button.bp3-outlined.bp3-intent-primary.bp3-disabled{
        background:none;
        color:rgba(16, 107, 163, 0.5); }
        .bp3-button.bp3-outlined.bp3-intent-primary:disabled.bp3-active, .bp3-button.bp3-outlined.bp3-intent-primary.bp3-disabled.bp3-active{
          background:rgba(19, 124, 189, 0.3); }
      .bp3-button.bp3-outlined.bp3-intent-primary .bp3-button-spinner .bp3-spinner-head{
        stroke:#106ba3; }
      .bp3-dark .bp3-button.bp3-outlined.bp3-intent-primary{
        color:#48aff0; }
        .bp3-dark .bp3-button.bp3-outlined.bp3-intent-primary:hover{
          background:rgba(19, 124, 189, 0.2);
          color:#48aff0; }
        .bp3-dark .bp3-button.bp3-outlined.bp3-intent-primary:active, .bp3-dark .bp3-button.bp3-outlined.bp3-intent-primary.bp3-active{
          background:rgba(19, 124, 189, 0.3);
          color:#48aff0; }
        .bp3-dark .bp3-button.bp3-outlined.bp3-intent-primary:disabled, .bp3-dark .bp3-button.bp3-outlined.bp3-intent-primary.bp3-disabled{
          background:none;
          color:rgba(72, 175, 240, 0.5); }
          .bp3-dark .bp3-button.bp3-outlined.bp3-intent-primary:disabled.bp3-active, .bp3-dark .bp3-button.bp3-outlined.bp3-intent-primary.bp3-disabled.bp3-active{
            background:rgba(19, 124, 189, 0.3); }
    .bp3-button.bp3-outlined.bp3-intent-success{
      color:#0d8050; }
      .bp3-button.bp3-outlined.bp3-intent-success:hover, .bp3-button.bp3-outlined.bp3-intent-success:active, .bp3-button.bp3-outlined.bp3-intent-success.bp3-active{
        background:none;
        -webkit-box-shadow:none;
                box-shadow:none;
        color:#0d8050; }
      .bp3-button.bp3-outlined.bp3-intent-success:hover{
        background:rgba(15, 153, 96, 0.15);
        color:#0d8050; }
      .bp3-button.bp3-outlined.bp3-intent-success:active, .bp3-button.bp3-outlined.bp3-intent-success.bp3-active{
        background:rgba(15, 153, 96, 0.3);
        color:#0d8050; }
      .bp3-button.bp3-outlined.bp3-intent-success:disabled, .bp3-button.bp3-outlined.bp3-intent-success.bp3-disabled{
        background:none;
        color:rgba(13, 128, 80, 0.5); }
        .bp3-button.bp3-outlined.bp3-intent-success:disabled.bp3-active, .bp3-button.bp3-outlined.bp3-intent-success.bp3-disabled.bp3-active{
          background:rgba(15, 153, 96, 0.3); }
      .bp3-button.bp3-outlined.bp3-intent-success .bp3-button-spinner .bp3-spinner-head{
        stroke:#0d8050; }
      .bp3-dark .bp3-button.bp3-outlined.bp3-intent-success{
        color:#3dcc91; }
        .bp3-dark .bp3-button.bp3-outlined.bp3-intent-success:hover{
          background:rgba(15, 153, 96, 0.2);
          color:#3dcc91; }
        .bp3-dark .bp3-button.bp3-outlined.bp3-intent-success:active, .bp3-dark .bp3-button.bp3-outlined.bp3-intent-success.bp3-active{
          background:rgba(15, 153, 96, 0.3);
          color:#3dcc91; }
        .bp3-dark .bp3-button.bp3-outlined.bp3-intent-success:disabled, .bp3-dark .bp3-button.bp3-outlined.bp3-intent-success.bp3-disabled{
          background:none;
          color:rgba(61, 204, 145, 0.5); }
          .bp3-dark .bp3-button.bp3-outlined.bp3-intent-success:disabled.bp3-active, .bp3-dark .bp3-button.bp3-outlined.bp3-intent-success.bp3-disabled.bp3-active{
            background:rgba(15, 153, 96, 0.3); }
    .bp3-button.bp3-outlined.bp3-intent-warning{
      color:#bf7326; }
      .bp3-button.bp3-outlined.bp3-intent-warning:hover, .bp3-button.bp3-outlined.bp3-intent-warning:active, .bp3-button.bp3-outlined.bp3-intent-warning.bp3-active{
        background:none;
        -webkit-box-shadow:none;
                box-shadow:none;
        color:#bf7326; }
      .bp3-button.bp3-outlined.bp3-intent-warning:hover{
        background:rgba(217, 130, 43, 0.15);
        color:#bf7326; }
      .bp3-button.bp3-outlined.bp3-intent-warning:active, .bp3-button.bp3-outlined.bp3-intent-warning.bp3-active{
        background:rgba(217, 130, 43, 0.3);
        color:#bf7326; }
      .bp3-button.bp3-outlined.bp3-intent-warning:disabled, .bp3-button.bp3-outlined.bp3-intent-warning.bp3-disabled{
        background:none;
        color:rgba(191, 115, 38, 0.5); }
        .bp3-button.bp3-outlined.bp3-intent-warning:disabled.bp3-active, .bp3-button.bp3-outlined.bp3-intent-warning.bp3-disabled.bp3-active{
          background:rgba(217, 130, 43, 0.3); }
      .bp3-button.bp3-outlined.bp3-intent-warning .bp3-button-spinner .bp3-spinner-head{
        stroke:#bf7326; }
      .bp3-dark .bp3-button.bp3-outlined.bp3-intent-warning{
        color:#ffb366; }
        .bp3-dark .bp3-button.bp3-outlined.bp3-intent-warning:hover{
          background:rgba(217, 130, 43, 0.2);
          color:#ffb366; }
        .bp3-dark .bp3-button.bp3-outlined.bp3-intent-warning:active, .bp3-dark .bp3-button.bp3-outlined.bp3-intent-warning.bp3-active{
          background:rgba(217, 130, 43, 0.3);
          color:#ffb366; }
        .bp3-dark .bp3-button.bp3-outlined.bp3-intent-warning:disabled, .bp3-dark .bp3-button.bp3-outlined.bp3-intent-warning.bp3-disabled{
          background:none;
          color:rgba(255, 179, 102, 0.5); }
          .bp3-dark .bp3-button.bp3-outlined.bp3-intent-warning:disabled.bp3-active, .bp3-dark .bp3-button.bp3-outlined.bp3-intent-warning.bp3-disabled.bp3-active{
            background:rgba(217, 130, 43, 0.3); }
    .bp3-button.bp3-outlined.bp3-intent-danger{
      color:#c23030; }
      .bp3-button.bp3-outlined.bp3-intent-danger:hover, .bp3-button.bp3-outlined.bp3-intent-danger:active, .bp3-button.bp3-outlined.bp3-intent-danger.bp3-active{
        background:none;
        -webkit-box-shadow:none;
                box-shadow:none;
        color:#c23030; }
      .bp3-button.bp3-outlined.bp3-intent-danger:hover{
        background:rgba(219, 55, 55, 0.15);
        color:#c23030; }
      .bp3-button.bp3-outlined.bp3-intent-danger:active, .bp3-button.bp3-outlined.bp3-intent-danger.bp3-active{
        background:rgba(219, 55, 55, 0.3);
        color:#c23030; }
      .bp3-button.bp3-outlined.bp3-intent-danger:disabled, .bp3-button.bp3-outlined.bp3-intent-danger.bp3-disabled{
        background:none;
        color:rgba(194, 48, 48, 0.5); }
        .bp3-button.bp3-outlined.bp3-intent-danger:disabled.bp3-active, .bp3-button.bp3-outlined.bp3-intent-danger.bp3-disabled.bp3-active{
          background:rgba(219, 55, 55, 0.3); }
      .bp3-button.bp3-outlined.bp3-intent-danger .bp3-button-spinner .bp3-spinner-head{
        stroke:#c23030; }
      .bp3-dark .bp3-button.bp3-outlined.bp3-intent-danger{
        color:#ff7373; }
        .bp3-dark .bp3-button.bp3-outlined.bp3-intent-danger:hover{
          background:rgba(219, 55, 55, 0.2);
          color:#ff7373; }
        .bp3-dark .bp3-button.bp3-outlined.bp3-intent-danger:active, .bp3-dark .bp3-button.bp3-outlined.bp3-intent-danger.bp3-active{
          background:rgba(219, 55, 55, 0.3);
          color:#ff7373; }
        .bp3-dark .bp3-button.bp3-outlined.bp3-intent-danger:disabled, .bp3-dark .bp3-button.bp3-outlined.bp3-intent-danger.bp3-disabled{
          background:none;
          color:rgba(255, 115, 115, 0.5); }
          .bp3-dark .bp3-button.bp3-outlined.bp3-intent-danger:disabled.bp3-active, .bp3-dark .bp3-button.bp3-outlined.bp3-intent-danger.bp3-disabled.bp3-active{
            background:rgba(219, 55, 55, 0.3); }
    .bp3-button.bp3-outlined:disabled, .bp3-button.bp3-outlined.bp3-disabled, .bp3-button.bp3-outlined:disabled:hover, .bp3-button.bp3-outlined.bp3-disabled:hover{
      border-color:rgba(92, 112, 128, 0.1); }
    .bp3-dark .bp3-button.bp3-outlined{
      border-color:rgba(255, 255, 255, 0.4); }
      .bp3-dark .bp3-button.bp3-outlined:disabled, .bp3-dark .bp3-button.bp3-outlined:disabled:hover, .bp3-dark .bp3-button.bp3-outlined.bp3-disabled, .bp3-dark .bp3-button.bp3-outlined.bp3-disabled:hover{
        border-color:rgba(255, 255, 255, 0.2); }
    .bp3-button.bp3-outlined.bp3-intent-primary{
      border-color:rgba(16, 107, 163, 0.6); }
      .bp3-button.bp3-outlined.bp3-intent-primary:disabled, .bp3-button.bp3-outlined.bp3-intent-primary.bp3-disabled{
        border-color:rgba(16, 107, 163, 0.2); }
      .bp3-dark .bp3-button.bp3-outlined.bp3-intent-primary{
        border-color:rgba(72, 175, 240, 0.6); }
        .bp3-dark .bp3-button.bp3-outlined.bp3-intent-primary:disabled, .bp3-dark .bp3-button.bp3-outlined.bp3-intent-primary.bp3-disabled{
          border-color:rgba(72, 175, 240, 0.2); }
    .bp3-button.bp3-outlined.bp3-intent-success{
      border-color:rgba(13, 128, 80, 0.6); }
      .bp3-button.bp3-outlined.bp3-intent-success:disabled, .bp3-button.bp3-outlined.bp3-intent-success.bp3-disabled{
        border-color:rgba(13, 128, 80, 0.2); }
      .bp3-dark .bp3-button.bp3-outlined.bp3-intent-success{
        border-color:rgba(61, 204, 145, 0.6); }
        .bp3-dark .bp3-button.bp3-outlined.bp3-intent-success:disabled, .bp3-dark .bp3-button.bp3-outlined.bp3-intent-success.bp3-disabled{
          border-color:rgba(61, 204, 145, 0.2); }
    .bp3-button.bp3-outlined.bp3-intent-warning{
      border-color:rgba(191, 115, 38, 0.6); }
      .bp3-button.bp3-outlined.bp3-intent-warning:disabled, .bp3-button.bp3-outlined.bp3-intent-warning.bp3-disabled{
        border-color:rgba(191, 115, 38, 0.2); }
      .bp3-dark .bp3-button.bp3-outlined.bp3-intent-warning{
        border-color:rgba(255, 179, 102, 0.6); }
        .bp3-dark .bp3-button.bp3-outlined.bp3-intent-warning:disabled, .bp3-dark .bp3-button.bp3-outlined.bp3-intent-warning.bp3-disabled{
          border-color:rgba(255, 179, 102, 0.2); }
    .bp3-button.bp3-outlined.bp3-intent-danger{
      border-color:rgba(194, 48, 48, 0.6); }
      .bp3-button.bp3-outlined.bp3-intent-danger:disabled, .bp3-button.bp3-outlined.bp3-intent-danger.bp3-disabled{
        border-color:rgba(194, 48, 48, 0.2); }
      .bp3-dark .bp3-button.bp3-outlined.bp3-intent-danger{
        border-color:rgba(255, 115, 115, 0.6); }
        .bp3-dark .bp3-button.bp3-outlined.bp3-intent-danger:disabled, .bp3-dark .bp3-button.bp3-outlined.bp3-intent-danger.bp3-disabled{
          border-color:rgba(255, 115, 115, 0.2); }

a.bp3-button{
  text-align:center;
  text-decoration:none;
  -webkit-transition:none;
  transition:none; }
  a.bp3-button, a.bp3-button:hover, a.bp3-button:active{
    color:#182026; }
  a.bp3-button.bp3-disabled{
    color:rgba(92, 112, 128, 0.6); }

.bp3-button-text{
  -webkit-box-flex:0;
      -ms-flex:0 1 auto;
          flex:0 1 auto; }

.bp3-button.bp3-align-left .bp3-button-text, .bp3-button.bp3-align-right .bp3-button-text,
.bp3-button-group.bp3-align-left .bp3-button-text,
.bp3-button-group.bp3-align-right .bp3-button-text{
  -webkit-box-flex:1;
      -ms-flex:1 1 auto;
          flex:1 1 auto; }
.bp3-button-group{
  display:-webkit-inline-box;
  display:-ms-inline-flexbox;
  display:inline-flex; }
  .bp3-button-group .bp3-button{
    -webkit-box-flex:0;
        -ms-flex:0 0 auto;
            flex:0 0 auto;
    position:relative;
    z-index:4; }
    .bp3-button-group .bp3-button:focus{
      z-index:5; }
    .bp3-button-group .bp3-button:hover{
      z-index:6; }
    .bp3-button-group .bp3-button:active, .bp3-button-group .bp3-button.bp3-active{
      z-index:7; }
    .bp3-button-group .bp3-button:disabled, .bp3-button-group .bp3-button.bp3-disabled{
      z-index:3; }
    .bp3-button-group .bp3-button[class*="bp3-intent-"]{
      z-index:9; }
      .bp3-button-group .bp3-button[class*="bp3-intent-"]:focus{
        z-index:10; }
      .bp3-button-group .bp3-button[class*="bp3-intent-"]:hover{
        z-index:11; }
      .bp3-button-group .bp3-button[class*="bp3-intent-"]:active, .bp3-button-group .bp3-button[class*="bp3-intent-"].bp3-active{
        z-index:12; }
      .bp3-button-group .bp3-button[class*="bp3-intent-"]:disabled, .bp3-button-group .bp3-button[class*="bp3-intent-"].bp3-disabled{
        z-index:8; }
  .bp3-button-group:not(.bp3-minimal) > .bp3-popover-wrapper:not(:first-child) .bp3-button,
  .bp3-button-group:not(.bp3-minimal) > .bp3-button:not(:first-child){
    border-bottom-left-radius:0;
    border-top-left-radius:0; }
  .bp3-button-group:not(.bp3-minimal) > .bp3-popover-wrapper:not(:last-child) .bp3-button,
  .bp3-button-group:not(.bp3-minimal) > .bp3-button:not(:last-child){
    border-bottom-right-radius:0;
    border-top-right-radius:0;
    margin-right:-1px; }
  .bp3-button-group.bp3-minimal .bp3-button{
    background:none;
    -webkit-box-shadow:none;
            box-shadow:none; }
    .bp3-button-group.bp3-minimal .bp3-button:hover{
      background:rgba(167, 182, 194, 0.3);
      -webkit-box-shadow:none;
              box-shadow:none;
      color:#182026;
      text-decoration:none; }
    .bp3-button-group.bp3-minimal .bp3-button:active, .bp3-button-group.bp3-minimal .bp3-button.bp3-active{
      background:rgba(115, 134, 148, 0.3);
      -webkit-box-shadow:none;
              box-shadow:none;
      color:#182026; }
    .bp3-button-group.bp3-minimal .bp3-button:disabled, .bp3-button-group.bp3-minimal .bp3-button:disabled:hover, .bp3-button-group.bp3-minimal .bp3-button.bp3-disabled, .bp3-button-group.bp3-minimal .bp3-button.bp3-disabled:hover{
      background:none;
      color:rgba(92, 112, 128, 0.6);
      cursor:not-allowed; }
      .bp3-button-group.bp3-minimal .bp3-button:disabled.bp3-active, .bp3-button-group.bp3-minimal .bp3-button:disabled:hover.bp3-active, .bp3-button-group.bp3-minimal .bp3-button.bp3-disabled.bp3-active, .bp3-button-group.bp3-minimal .bp3-button.bp3-disabled:hover.bp3-active{
        background:rgba(115, 134, 148, 0.3); }
    .bp3-dark .bp3-button-group.bp3-minimal .bp3-button{
      background:none;
      -webkit-box-shadow:none;
              box-shadow:none;
      color:inherit; }
      .bp3-dark .bp3-button-group.bp3-minimal .bp3-button:hover, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button:active, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-active{
        background:none;
        -webkit-box-shadow:none;
                box-shadow:none; }
      .bp3-dark .bp3-button-group.bp3-minimal .bp3-button:hover{
        background:rgba(138, 155, 168, 0.15); }
      .bp3-dark .bp3-button-group.bp3-minimal .bp3-button:active, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-active{
        background:rgba(138, 155, 168, 0.3);
        color:#f5f8fa; }
      .bp3-dark .bp3-button-group.bp3-minimal .bp3-button:disabled, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button:disabled:hover, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-disabled, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-disabled:hover{
        background:none;
        color:rgba(167, 182, 194, 0.6);
        cursor:not-allowed; }
        .bp3-dark .bp3-button-group.bp3-minimal .bp3-button:disabled.bp3-active, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button:disabled:hover.bp3-active, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-disabled.bp3-active, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-disabled:hover.bp3-active{
          background:rgba(138, 155, 168, 0.3); }
    .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary{
      color:#106ba3; }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary:hover, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary:active, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary.bp3-active{
        background:none;
        -webkit-box-shadow:none;
                box-shadow:none;
        color:#106ba3; }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary:hover{
        background:rgba(19, 124, 189, 0.15);
        color:#106ba3; }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary:active, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary.bp3-active{
        background:rgba(19, 124, 189, 0.3);
        color:#106ba3; }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary:disabled, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary.bp3-disabled{
        background:none;
        color:rgba(16, 107, 163, 0.5); }
        .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary:disabled.bp3-active, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary.bp3-disabled.bp3-active{
          background:rgba(19, 124, 189, 0.3); }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary .bp3-button-spinner .bp3-spinner-head{
        stroke:#106ba3; }
      .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary{
        color:#48aff0; }
        .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary:hover{
          background:rgba(19, 124, 189, 0.2);
          color:#48aff0; }
        .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary:active, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary.bp3-active{
          background:rgba(19, 124, 189, 0.3);
          color:#48aff0; }
        .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary:disabled, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary.bp3-disabled{
          background:none;
          color:rgba(72, 175, 240, 0.5); }
          .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary:disabled.bp3-active, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-primary.bp3-disabled.bp3-active{
            background:rgba(19, 124, 189, 0.3); }
    .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success{
      color:#0d8050; }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success:hover, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success:active, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success.bp3-active{
        background:none;
        -webkit-box-shadow:none;
                box-shadow:none;
        color:#0d8050; }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success:hover{
        background:rgba(15, 153, 96, 0.15);
        color:#0d8050; }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success:active, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success.bp3-active{
        background:rgba(15, 153, 96, 0.3);
        color:#0d8050; }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success:disabled, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success.bp3-disabled{
        background:none;
        color:rgba(13, 128, 80, 0.5); }
        .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success:disabled.bp3-active, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success.bp3-disabled.bp3-active{
          background:rgba(15, 153, 96, 0.3); }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success .bp3-button-spinner .bp3-spinner-head{
        stroke:#0d8050; }
      .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success{
        color:#3dcc91; }
        .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success:hover{
          background:rgba(15, 153, 96, 0.2);
          color:#3dcc91; }
        .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success:active, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success.bp3-active{
          background:rgba(15, 153, 96, 0.3);
          color:#3dcc91; }
        .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success:disabled, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success.bp3-disabled{
          background:none;
          color:rgba(61, 204, 145, 0.5); }
          .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success:disabled.bp3-active, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-success.bp3-disabled.bp3-active{
            background:rgba(15, 153, 96, 0.3); }
    .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning{
      color:#bf7326; }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning:hover, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning:active, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning.bp3-active{
        background:none;
        -webkit-box-shadow:none;
                box-shadow:none;
        color:#bf7326; }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning:hover{
        background:rgba(217, 130, 43, 0.15);
        color:#bf7326; }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning:active, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning.bp3-active{
        background:rgba(217, 130, 43, 0.3);
        color:#bf7326; }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning:disabled, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning.bp3-disabled{
        background:none;
        color:rgba(191, 115, 38, 0.5); }
        .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning:disabled.bp3-active, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning.bp3-disabled.bp3-active{
          background:rgba(217, 130, 43, 0.3); }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning .bp3-button-spinner .bp3-spinner-head{
        stroke:#bf7326; }
      .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning{
        color:#ffb366; }
        .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning:hover{
          background:rgba(217, 130, 43, 0.2);
          color:#ffb366; }
        .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning:active, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning.bp3-active{
          background:rgba(217, 130, 43, 0.3);
          color:#ffb366; }
        .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning:disabled, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning.bp3-disabled{
          background:none;
          color:rgba(255, 179, 102, 0.5); }
          .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning:disabled.bp3-active, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-warning.bp3-disabled.bp3-active{
            background:rgba(217, 130, 43, 0.3); }
    .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger{
      color:#c23030; }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger:hover, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger:active, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger.bp3-active{
        background:none;
        -webkit-box-shadow:none;
                box-shadow:none;
        color:#c23030; }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger:hover{
        background:rgba(219, 55, 55, 0.15);
        color:#c23030; }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger:active, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger.bp3-active{
        background:rgba(219, 55, 55, 0.3);
        color:#c23030; }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger:disabled, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger.bp3-disabled{
        background:none;
        color:rgba(194, 48, 48, 0.5); }
        .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger:disabled.bp3-active, .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger.bp3-disabled.bp3-active{
          background:rgba(219, 55, 55, 0.3); }
      .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger .bp3-button-spinner .bp3-spinner-head{
        stroke:#c23030; }
      .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger{
        color:#ff7373; }
        .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger:hover{
          background:rgba(219, 55, 55, 0.2);
          color:#ff7373; }
        .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger:active, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger.bp3-active{
          background:rgba(219, 55, 55, 0.3);
          color:#ff7373; }
        .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger:disabled, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger.bp3-disabled{
          background:none;
          color:rgba(255, 115, 115, 0.5); }
          .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger:disabled.bp3-active, .bp3-dark .bp3-button-group.bp3-minimal .bp3-button.bp3-intent-danger.bp3-disabled.bp3-active{
            background:rgba(219, 55, 55, 0.3); }
  .bp3-button-group .bp3-popover-wrapper,
  .bp3-button-group .bp3-popover-target{
    display:-webkit-box;
    display:-ms-flexbox;
    display:flex;
    -webkit-box-flex:1;
        -ms-flex:1 1 auto;
            flex:1 1 auto; }
  .bp3-button-group.bp3-fill{
    display:-webkit-box;
    display:-ms-flexbox;
    display:flex;
    width:100%; }
  .bp3-button-group .bp3-button.bp3-fill,
  .bp3-button-group.bp3-fill .bp3-button:not(.bp3-fixed){
    -webkit-box-flex:1;
        -ms-flex:1 1 auto;
            flex:1 1 auto; }
  .bp3-button-group.bp3-vertical{
    -webkit-box-align:stretch;
        -ms-flex-align:stretch;
            align-items:stretch;
    -webkit-box-orient:vertical;
    -webkit-box-direction:normal;
        -ms-flex-direction:column;
            flex-direction:column;
    vertical-align:top; }
    .bp3-button-group.bp3-vertical.bp3-fill{
      height:100%;
      width:unset; }
    .bp3-button-group.bp3-vertical .bp3-button{
      margin-right:0 !important;
      width:100%; }
    .bp3-button-group.bp3-vertical:not(.bp3-minimal) > .bp3-popover-wrapper:first-child .bp3-button,
    .bp3-button-group.bp3-vertical:not(.bp3-minimal) > .bp3-button:first-child{
      border-radius:3px 3px 0 0; }
    .bp3-button-group.bp3-vertical:not(.bp3-minimal) > .bp3-popover-wrapper:last-child .bp3-button,
    .bp3-button-group.bp3-vertical:not(.bp3-minimal) > .bp3-button:last-child{
      border-radius:0 0 3px 3px; }
    .bp3-button-group.bp3-vertical:not(.bp3-minimal) > .bp3-popover-wrapper:not(:last-child) .bp3-button,
    .bp3-button-group.bp3-vertical:not(.bp3-minimal) > .bp3-button:not(:last-child){
      margin-bottom:-1px; }
  .bp3-button-group.bp3-align-left .bp3-button{
    text-align:left; }
  .bp3-dark .bp3-button-group:not(.bp3-minimal) > .bp3-popover-wrapper:not(:last-child) .bp3-button,
  .bp3-dark .bp3-button-group:not(.bp3-minimal) > .bp3-button:not(:last-child){
    margin-right:1px; }
  .bp3-dark .bp3-button-group.bp3-vertical > .bp3-popover-wrapper:not(:last-child) .bp3-button,
  .bp3-dark .bp3-button-group.bp3-vertical > .bp3-button:not(:last-child){
    margin-bottom:1px; }
.bp3-callout{
  font-size:14px;
  line-height:1.5;
  background-color:rgba(138, 155, 168, 0.15);
  border-radius:3px;
  padding:10px 12px 9px;
  position:relative;
  width:100%; }
  .bp3-callout[class*="bp3-icon-"]{
    padding-left:40px; }
    .bp3-callout[class*="bp3-icon-"]::before{
      font-family:"Icons20", sans-serif;
      font-size:20px;
      font-style:normal;
      font-weight:400;
      line-height:1;
      -moz-osx-font-smoothing:grayscale;
      -webkit-font-smoothing:antialiased;
      color:#5c7080;
      left:10px;
      position:absolute;
      top:10px; }
  .bp3-callout.bp3-callout-icon{
    padding-left:40px; }
    .bp3-callout.bp3-callout-icon > .bp3-icon:first-child{
      color:#5c7080;
      left:10px;
      position:absolute;
      top:10px; }
  .bp3-callout .bp3-heading{
    line-height:20px;
    margin-bottom:5px;
    margin-top:0; }
    .bp3-callout .bp3-heading:last-child{
      margin-bottom:0; }
  .bp3-dark .bp3-callout{
    background-color:rgba(138, 155, 168, 0.2); }
    .bp3-dark .bp3-callout[class*="bp3-icon-"]::before{
      color:#a7b6c2; }
  .bp3-callout.bp3-intent-primary{
    background-color:rgba(19, 124, 189, 0.15); }
    .bp3-callout.bp3-intent-primary[class*="bp3-icon-"]::before,
    .bp3-callout.bp3-intent-primary > .bp3-icon:first-child,
    .bp3-callout.bp3-intent-primary .bp3-heading{
      color:#106ba3; }
    .bp3-dark .bp3-callout.bp3-intent-primary{
      background-color:rgba(19, 124, 189, 0.25); }
      .bp3-dark .bp3-callout.bp3-intent-primary[class*="bp3-icon-"]::before,
      .bp3-dark .bp3-callout.bp3-intent-primary > .bp3-icon:first-child,
      .bp3-dark .bp3-callout.bp3-intent-primary .bp3-heading{
        color:#48aff0; }
  .bp3-callout.bp3-intent-success{
    background-color:rgba(15, 153, 96, 0.15); }
    .bp3-callout.bp3-intent-success[class*="bp3-icon-"]::before,
    .bp3-callout.bp3-intent-success > .bp3-icon:first-child,
    .bp3-callout.bp3-intent-success .bp3-heading{
      color:#0d8050; }
    .bp3-dark .bp3-callout.bp3-intent-success{
      background-color:rgba(15, 153, 96, 0.25); }
      .bp3-dark .bp3-callout.bp3-intent-success[class*="bp3-icon-"]::before,
      .bp3-dark .bp3-callout.bp3-intent-success > .bp3-icon:first-child,
      .bp3-dark .bp3-callout.bp3-intent-success .bp3-heading{
        color:#3dcc91; }
  .bp3-callout.bp3-intent-warning{
    background-color:rgba(217, 130, 43, 0.15); }
    .bp3-callout.bp3-intent-warning[class*="bp3-icon-"]::before,
    .bp3-callout.bp3-intent-warning > .bp3-icon:first-child,
    .bp3-callout.bp3-intent-warning .bp3-heading{
      color:#bf7326; }
    .bp3-dark .bp3-callout.bp3-intent-warning{
      background-color:rgba(217, 130, 43, 0.25); }
      .bp3-dark .bp3-callout.bp3-intent-warning[class*="bp3-icon-"]::before,
      .bp3-dark .bp3-callout.bp3-intent-warning > .bp3-icon:first-child,
      .bp3-dark .bp3-callout.bp3-intent-warning .bp3-heading{
        color:#ffb366; }
  .bp3-callout.bp3-intent-danger{
    background-color:rgba(219, 55, 55, 0.15); }
    .bp3-callout.bp3-intent-danger[class*="bp3-icon-"]::before,
    .bp3-callout.bp3-intent-danger > .bp3-icon:first-child,
    .bp3-callout.bp3-intent-danger .bp3-heading{
      color:#c23030; }
    .bp3-dark .bp3-callout.bp3-intent-danger{
      background-color:rgba(219, 55, 55, 0.25); }
      .bp3-dark .bp3-callout.bp3-intent-danger[class*="bp3-icon-"]::before,
      .bp3-dark .bp3-callout.bp3-intent-danger > .bp3-icon:first-child,
      .bp3-dark .bp3-callout.bp3-intent-danger .bp3-heading{
        color:#ff7373; }
  .bp3-running-text .bp3-callout{
    margin:20px 0; }
.bp3-card{
  background-color:#ffffff;
  border-radius:3px;
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.15), 0 0 0 rgba(16, 22, 26, 0), 0 0 0 rgba(16, 22, 26, 0);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.15), 0 0 0 rgba(16, 22, 26, 0), 0 0 0 rgba(16, 22, 26, 0);
  padding:20px;
  -webkit-transition:-webkit-transform 200ms cubic-bezier(0.4, 1, 0.75, 0.9), -webkit-box-shadow 200ms cubic-bezier(0.4, 1, 0.75, 0.9);
  transition:-webkit-transform 200ms cubic-bezier(0.4, 1, 0.75, 0.9), -webkit-box-shadow 200ms cubic-bezier(0.4, 1, 0.75, 0.9);
  transition:transform 200ms cubic-bezier(0.4, 1, 0.75, 0.9), box-shadow 200ms cubic-bezier(0.4, 1, 0.75, 0.9);
  transition:transform 200ms cubic-bezier(0.4, 1, 0.75, 0.9), box-shadow 200ms cubic-bezier(0.4, 1, 0.75, 0.9), -webkit-transform 200ms cubic-bezier(0.4, 1, 0.75, 0.9), -webkit-box-shadow 200ms cubic-bezier(0.4, 1, 0.75, 0.9); }
  .bp3-card.bp3-dark,
  .bp3-dark .bp3-card{
    background-color:#30404d;
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4), 0 0 0 rgba(16, 22, 26, 0), 0 0 0 rgba(16, 22, 26, 0);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4), 0 0 0 rgba(16, 22, 26, 0), 0 0 0 rgba(16, 22, 26, 0); }

.bp3-elevation-0{
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.15), 0 0 0 rgba(16, 22, 26, 0), 0 0 0 rgba(16, 22, 26, 0);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.15), 0 0 0 rgba(16, 22, 26, 0), 0 0 0 rgba(16, 22, 26, 0); }
  .bp3-elevation-0.bp3-dark,
  .bp3-dark .bp3-elevation-0{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4), 0 0 0 rgba(16, 22, 26, 0), 0 0 0 rgba(16, 22, 26, 0);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4), 0 0 0 rgba(16, 22, 26, 0), 0 0 0 rgba(16, 22, 26, 0); }

.bp3-elevation-1{
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.2);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.2); }
  .bp3-elevation-1.bp3-dark,
  .bp3-dark .bp3-elevation-1{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.4); }

.bp3-elevation-2{
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 1px 1px rgba(16, 22, 26, 0.2), 0 2px 6px rgba(16, 22, 26, 0.2);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 1px 1px rgba(16, 22, 26, 0.2), 0 2px 6px rgba(16, 22, 26, 0.2); }
  .bp3-elevation-2.bp3-dark,
  .bp3-dark .bp3-elevation-2{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 1px 1px rgba(16, 22, 26, 0.4), 0 2px 6px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 1px 1px rgba(16, 22, 26, 0.4), 0 2px 6px rgba(16, 22, 26, 0.4); }

.bp3-elevation-3{
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 2px 4px rgba(16, 22, 26, 0.2), 0 8px 24px rgba(16, 22, 26, 0.2);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 2px 4px rgba(16, 22, 26, 0.2), 0 8px 24px rgba(16, 22, 26, 0.2); }
  .bp3-elevation-3.bp3-dark,
  .bp3-dark .bp3-elevation-3{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 2px 4px rgba(16, 22, 26, 0.4), 0 8px 24px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 2px 4px rgba(16, 22, 26, 0.4), 0 8px 24px rgba(16, 22, 26, 0.4); }

.bp3-elevation-4{
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 4px 8px rgba(16, 22, 26, 0.2), 0 18px 46px 6px rgba(16, 22, 26, 0.2);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 4px 8px rgba(16, 22, 26, 0.2), 0 18px 46px 6px rgba(16, 22, 26, 0.2); }
  .bp3-elevation-4.bp3-dark,
  .bp3-dark .bp3-elevation-4{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 4px 8px rgba(16, 22, 26, 0.4), 0 18px 46px 6px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 4px 8px rgba(16, 22, 26, 0.4), 0 18px 46px 6px rgba(16, 22, 26, 0.4); }

.bp3-card.bp3-interactive:hover{
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 2px 4px rgba(16, 22, 26, 0.2), 0 8px 24px rgba(16, 22, 26, 0.2);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 2px 4px rgba(16, 22, 26, 0.2), 0 8px 24px rgba(16, 22, 26, 0.2);
  cursor:pointer; }
  .bp3-card.bp3-interactive:hover.bp3-dark,
  .bp3-dark .bp3-card.bp3-interactive:hover{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 2px 4px rgba(16, 22, 26, 0.4), 0 8px 24px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 2px 4px rgba(16, 22, 26, 0.4), 0 8px 24px rgba(16, 22, 26, 0.4); }

.bp3-card.bp3-interactive:active{
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.2);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.2);
  opacity:0.9;
  -webkit-transition-duration:0;
          transition-duration:0; }
  .bp3-card.bp3-interactive:active.bp3-dark,
  .bp3-dark .bp3-card.bp3-interactive:active{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.4); }

.bp3-collapse{
  height:0;
  overflow-y:hidden;
  -webkit-transition:height 200ms cubic-bezier(0.4, 1, 0.75, 0.9);
  transition:height 200ms cubic-bezier(0.4, 1, 0.75, 0.9); }
  .bp3-collapse .bp3-collapse-body{
    -webkit-transition:-webkit-transform 200ms cubic-bezier(0.4, 1, 0.75, 0.9);
    transition:-webkit-transform 200ms cubic-bezier(0.4, 1, 0.75, 0.9);
    transition:transform 200ms cubic-bezier(0.4, 1, 0.75, 0.9);
    transition:transform 200ms cubic-bezier(0.4, 1, 0.75, 0.9), -webkit-transform 200ms cubic-bezier(0.4, 1, 0.75, 0.9); }
    .bp3-collapse .bp3-collapse-body[aria-hidden="true"]{
      display:none; }

.bp3-context-menu .bp3-popover-target{
  display:block; }

.bp3-context-menu-popover-target{
  position:fixed; }

.bp3-divider{
  border-bottom:1px solid rgba(16, 22, 26, 0.15);
  border-right:1px solid rgba(16, 22, 26, 0.15);
  margin:5px; }
  .bp3-dark .bp3-divider{
    border-color:rgba(16, 22, 26, 0.4); }
.bp3-dialog-container{
  opacity:1;
  -webkit-transform:scale(1);
          transform:scale(1);
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center;
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-pack:center;
      -ms-flex-pack:center;
          justify-content:center;
  min-height:100%;
  pointer-events:none;
  -webkit-user-select:none;
     -moz-user-select:none;
      -ms-user-select:none;
          user-select:none;
  width:100%; }
  .bp3-dialog-container.bp3-overlay-enter > .bp3-dialog, .bp3-dialog-container.bp3-overlay-appear > .bp3-dialog{
    opacity:0;
    -webkit-transform:scale(0.5);
            transform:scale(0.5); }
  .bp3-dialog-container.bp3-overlay-enter-active > .bp3-dialog, .bp3-dialog-container.bp3-overlay-appear-active > .bp3-dialog{
    opacity:1;
    -webkit-transform:scale(1);
            transform:scale(1);
    -webkit-transition-delay:0;
            transition-delay:0;
    -webkit-transition-duration:300ms;
            transition-duration:300ms;
    -webkit-transition-property:opacity, -webkit-transform;
    transition-property:opacity, -webkit-transform;
    transition-property:opacity, transform;
    transition-property:opacity, transform, -webkit-transform;
    -webkit-transition-timing-function:cubic-bezier(0.54, 1.12, 0.38, 1.11);
            transition-timing-function:cubic-bezier(0.54, 1.12, 0.38, 1.11); }
  .bp3-dialog-container.bp3-overlay-exit > .bp3-dialog{
    opacity:1;
    -webkit-transform:scale(1);
            transform:scale(1); }
  .bp3-dialog-container.bp3-overlay-exit-active > .bp3-dialog{
    opacity:0;
    -webkit-transform:scale(0.5);
            transform:scale(0.5);
    -webkit-transition-delay:0;
            transition-delay:0;
    -webkit-transition-duration:300ms;
            transition-duration:300ms;
    -webkit-transition-property:opacity, -webkit-transform;
    transition-property:opacity, -webkit-transform;
    transition-property:opacity, transform;
    transition-property:opacity, transform, -webkit-transform;
    -webkit-transition-timing-function:cubic-bezier(0.54, 1.12, 0.38, 1.11);
            transition-timing-function:cubic-bezier(0.54, 1.12, 0.38, 1.11); }

.bp3-dialog{
  background:#ebf1f5;
  border-radius:6px;
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 4px 8px rgba(16, 22, 26, 0.2), 0 18px 46px 6px rgba(16, 22, 26, 0.2);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 4px 8px rgba(16, 22, 26, 0.2), 0 18px 46px 6px rgba(16, 22, 26, 0.2);
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-orient:vertical;
  -webkit-box-direction:normal;
      -ms-flex-direction:column;
          flex-direction:column;
  margin:30px 0;
  padding-bottom:20px;
  pointer-events:all;
  -webkit-user-select:text;
     -moz-user-select:text;
      -ms-user-select:text;
          user-select:text;
  width:500px; }
  .bp3-dialog:focus{
    outline:0; }
  .bp3-dialog.bp3-dark,
  .bp3-dark .bp3-dialog{
    background:#293742;
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 4px 8px rgba(16, 22, 26, 0.4), 0 18px 46px 6px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 4px 8px rgba(16, 22, 26, 0.4), 0 18px 46px 6px rgba(16, 22, 26, 0.4);
    color:#f5f8fa; }

.bp3-dialog-header{
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center;
  background:#ffffff;
  border-radius:6px 6px 0 0;
  -webkit-box-shadow:0 1px 0 rgba(16, 22, 26, 0.15);
          box-shadow:0 1px 0 rgba(16, 22, 26, 0.15);
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-flex:0;
      -ms-flex:0 0 auto;
          flex:0 0 auto;
  min-height:40px;
  padding-left:20px;
  padding-right:5px;
  z-index:30; }
  .bp3-dialog-header .bp3-icon-large,
  .bp3-dialog-header .bp3-icon{
    color:#5c7080;
    -webkit-box-flex:0;
        -ms-flex:0 0 auto;
            flex:0 0 auto;
    margin-right:10px; }
  .bp3-dialog-header .bp3-heading{
    overflow:hidden;
    text-overflow:ellipsis;
    white-space:nowrap;
    word-wrap:normal;
    -webkit-box-flex:1;
        -ms-flex:1 1 auto;
            flex:1 1 auto;
    line-height:inherit;
    margin:0; }
    .bp3-dialog-header .bp3-heading:last-child{
      margin-right:20px; }
  .bp3-dark .bp3-dialog-header{
    background:#30404d;
    -webkit-box-shadow:0 1px 0 rgba(16, 22, 26, 0.4);
            box-shadow:0 1px 0 rgba(16, 22, 26, 0.4); }
    .bp3-dark .bp3-dialog-header .bp3-icon-large,
    .bp3-dark .bp3-dialog-header .bp3-icon{
      color:#a7b6c2; }

.bp3-dialog-body{
  -webkit-box-flex:1;
      -ms-flex:1 1 auto;
          flex:1 1 auto;
  line-height:18px;
  margin:20px; }

.bp3-dialog-footer{
  -webkit-box-flex:0;
      -ms-flex:0 0 auto;
          flex:0 0 auto;
  margin:0 20px; }

.bp3-dialog-footer-actions{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-pack:end;
      -ms-flex-pack:end;
          justify-content:flex-end; }
  .bp3-dialog-footer-actions .bp3-button{
    margin-left:10px; }
.bp3-multistep-dialog-panels{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex; }

.bp3-multistep-dialog-left-panel{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-flex:1;
      -ms-flex:1;
          flex:1;
  -webkit-box-orient:vertical;
  -webkit-box-direction:normal;
      -ms-flex-direction:column;
          flex-direction:column; }
  .bp3-dark .bp3-multistep-dialog-left-panel{
    background:#202b33; }

.bp3-multistep-dialog-right-panel{
  background-color:#f5f8fa;
  border-left:1px solid rgba(16, 22, 26, 0.15);
  border-radius:0 0 6px 0;
  -webkit-box-flex:3;
      -ms-flex:3;
          flex:3;
  min-width:0; }
  .bp3-dark .bp3-multistep-dialog-right-panel{
    background-color:#293742;
    border-left:1px solid rgba(16, 22, 26, 0.4); }

.bp3-multistep-dialog-footer{
  background-color:#ffffff;
  border-radius:0 0 6px 0;
  border-top:1px solid rgba(16, 22, 26, 0.15);
  padding:10px; }
  .bp3-dark .bp3-multistep-dialog-footer{
    background:#30404d;
    border-top:1px solid rgba(16, 22, 26, 0.4); }

.bp3-dialog-step-container{
  background-color:#f5f8fa;
  border-bottom:1px solid rgba(16, 22, 26, 0.15); }
  .bp3-dark .bp3-dialog-step-container{
    background:#293742;
    border-bottom:1px solid rgba(16, 22, 26, 0.4); }
  .bp3-dialog-step-container.bp3-dialog-step-viewed{
    background-color:#ffffff; }
    .bp3-dark .bp3-dialog-step-container.bp3-dialog-step-viewed{
      background:#30404d; }

.bp3-dialog-step{
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center;
  background-color:#f5f8fa;
  border-radius:6px;
  cursor:not-allowed;
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  margin:4px;
  padding:6px 14px; }
  .bp3-dark .bp3-dialog-step{
    background:#293742; }
  .bp3-dialog-step-viewed .bp3-dialog-step{
    background-color:#ffffff;
    cursor:pointer; }
    .bp3-dark .bp3-dialog-step-viewed .bp3-dialog-step{
      background:#30404d; }
  .bp3-dialog-step:hover{
    background-color:#f5f8fa; }
    .bp3-dark .bp3-dialog-step:hover{
      background:#293742; }

.bp3-dialog-step-icon{
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center;
  background-color:rgba(92, 112, 128, 0.6);
  border-radius:50%;
  color:#ffffff;
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  height:25px;
  -webkit-box-pack:center;
      -ms-flex-pack:center;
          justify-content:center;
  width:25px; }
  .bp3-dark .bp3-dialog-step-icon{
    background-color:rgba(167, 182, 194, 0.6); }
  .bp3-active.bp3-dialog-step-viewed .bp3-dialog-step-icon{
    background-color:#2b95d6; }
  .bp3-dialog-step-viewed .bp3-dialog-step-icon{
    background-color:#8a9ba8; }

.bp3-dialog-step-title{
  color:rgba(92, 112, 128, 0.6);
  -webkit-box-flex:1;
      -ms-flex:1;
          flex:1;
  padding-left:10px; }
  .bp3-dark .bp3-dialog-step-title{
    color:rgba(167, 182, 194, 0.6); }
  .bp3-active.bp3-dialog-step-viewed .bp3-dialog-step-title{
    color:#2b95d6; }
  .bp3-dialog-step-viewed:not(.bp3-active) .bp3-dialog-step-title{
    color:#182026; }
    .bp3-dark .bp3-dialog-step-viewed:not(.bp3-active) .bp3-dialog-step-title{
      color:#f5f8fa; }
.bp3-drawer{
  background:#ffffff;
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 4px 8px rgba(16, 22, 26, 0.2), 0 18px 46px 6px rgba(16, 22, 26, 0.2);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 4px 8px rgba(16, 22, 26, 0.2), 0 18px 46px 6px rgba(16, 22, 26, 0.2);
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-orient:vertical;
  -webkit-box-direction:normal;
      -ms-flex-direction:column;
          flex-direction:column;
  margin:0;
  padding:0; }
  .bp3-drawer:focus{
    outline:0; }
  .bp3-drawer.bp3-position-top{
    height:50%;
    left:0;
    right:0;
    top:0; }
    .bp3-drawer.bp3-position-top.bp3-overlay-enter, .bp3-drawer.bp3-position-top.bp3-overlay-appear{
      -webkit-transform:translateY(-100%);
              transform:translateY(-100%); }
    .bp3-drawer.bp3-position-top.bp3-overlay-enter-active, .bp3-drawer.bp3-position-top.bp3-overlay-appear-active{
      -webkit-transform:translateY(0);
              transform:translateY(0);
      -webkit-transition-delay:0;
              transition-delay:0;
      -webkit-transition-duration:200ms;
              transition-duration:200ms;
      -webkit-transition-property:-webkit-transform;
      transition-property:-webkit-transform;
      transition-property:transform;
      transition-property:transform, -webkit-transform;
      -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
              transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9); }
    .bp3-drawer.bp3-position-top.bp3-overlay-exit{
      -webkit-transform:translateY(0);
              transform:translateY(0); }
    .bp3-drawer.bp3-position-top.bp3-overlay-exit-active{
      -webkit-transform:translateY(-100%);
              transform:translateY(-100%);
      -webkit-transition-delay:0;
              transition-delay:0;
      -webkit-transition-duration:100ms;
              transition-duration:100ms;
      -webkit-transition-property:-webkit-transform;
      transition-property:-webkit-transform;
      transition-property:transform;
      transition-property:transform, -webkit-transform;
      -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
              transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9); }
  .bp3-drawer.bp3-position-bottom{
    bottom:0;
    height:50%;
    left:0;
    right:0; }
    .bp3-drawer.bp3-position-bottom.bp3-overlay-enter, .bp3-drawer.bp3-position-bottom.bp3-overlay-appear{
      -webkit-transform:translateY(100%);
              transform:translateY(100%); }
    .bp3-drawer.bp3-position-bottom.bp3-overlay-enter-active, .bp3-drawer.bp3-position-bottom.bp3-overlay-appear-active{
      -webkit-transform:translateY(0);
              transform:translateY(0);
      -webkit-transition-delay:0;
              transition-delay:0;
      -webkit-transition-duration:200ms;
              transition-duration:200ms;
      -webkit-transition-property:-webkit-transform;
      transition-property:-webkit-transform;
      transition-property:transform;
      transition-property:transform, -webkit-transform;
      -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
              transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9); }
    .bp3-drawer.bp3-position-bottom.bp3-overlay-exit{
      -webkit-transform:translateY(0);
              transform:translateY(0); }
    .bp3-drawer.bp3-position-bottom.bp3-overlay-exit-active{
      -webkit-transform:translateY(100%);
              transform:translateY(100%);
      -webkit-transition-delay:0;
              transition-delay:0;
      -webkit-transition-duration:100ms;
              transition-duration:100ms;
      -webkit-transition-property:-webkit-transform;
      transition-property:-webkit-transform;
      transition-property:transform;
      transition-property:transform, -webkit-transform;
      -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
              transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9); }
  .bp3-drawer.bp3-position-left{
    bottom:0;
    left:0;
    top:0;
    width:50%; }
    .bp3-drawer.bp3-position-left.bp3-overlay-enter, .bp3-drawer.bp3-position-left.bp3-overlay-appear{
      -webkit-transform:translateX(-100%);
              transform:translateX(-100%); }
    .bp3-drawer.bp3-position-left.bp3-overlay-enter-active, .bp3-drawer.bp3-position-left.bp3-overlay-appear-active{
      -webkit-transform:translateX(0);
              transform:translateX(0);
      -webkit-transition-delay:0;
              transition-delay:0;
      -webkit-transition-duration:200ms;
              transition-duration:200ms;
      -webkit-transition-property:-webkit-transform;
      transition-property:-webkit-transform;
      transition-property:transform;
      transition-property:transform, -webkit-transform;
      -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
              transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9); }
    .bp3-drawer.bp3-position-left.bp3-overlay-exit{
      -webkit-transform:translateX(0);
              transform:translateX(0); }
    .bp3-drawer.bp3-position-left.bp3-overlay-exit-active{
      -webkit-transform:translateX(-100%);
              transform:translateX(-100%);
      -webkit-transition-delay:0;
              transition-delay:0;
      -webkit-transition-duration:100ms;
              transition-duration:100ms;
      -webkit-transition-property:-webkit-transform;
      transition-property:-webkit-transform;
      transition-property:transform;
      transition-property:transform, -webkit-transform;
      -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
              transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9); }
  .bp3-drawer.bp3-position-right{
    bottom:0;
    right:0;
    top:0;
    width:50%; }
    .bp3-drawer.bp3-position-right.bp3-overlay-enter, .bp3-drawer.bp3-position-right.bp3-overlay-appear{
      -webkit-transform:translateX(100%);
              transform:translateX(100%); }
    .bp3-drawer.bp3-position-right.bp3-overlay-enter-active, .bp3-drawer.bp3-position-right.bp3-overlay-appear-active{
      -webkit-transform:translateX(0);
              transform:translateX(0);
      -webkit-transition-delay:0;
              transition-delay:0;
      -webkit-transition-duration:200ms;
              transition-duration:200ms;
      -webkit-transition-property:-webkit-transform;
      transition-property:-webkit-transform;
      transition-property:transform;
      transition-property:transform, -webkit-transform;
      -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
              transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9); }
    .bp3-drawer.bp3-position-right.bp3-overlay-exit{
      -webkit-transform:translateX(0);
              transform:translateX(0); }
    .bp3-drawer.bp3-position-right.bp3-overlay-exit-active{
      -webkit-transform:translateX(100%);
              transform:translateX(100%);
      -webkit-transition-delay:0;
              transition-delay:0;
      -webkit-transition-duration:100ms;
              transition-duration:100ms;
      -webkit-transition-property:-webkit-transform;
      transition-property:-webkit-transform;
      transition-property:transform;
      transition-property:transform, -webkit-transform;
      -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
              transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9); }
  .bp3-drawer:not(.bp3-position-top):not(.bp3-position-bottom):not(.bp3-position-left):not(
  .bp3-position-right):not(.bp3-vertical){
    bottom:0;
    right:0;
    top:0;
    width:50%; }
    .bp3-drawer:not(.bp3-position-top):not(.bp3-position-bottom):not(.bp3-position-left):not(
    .bp3-position-right):not(.bp3-vertical).bp3-overlay-enter, .bp3-drawer:not(.bp3-position-top):not(.bp3-position-bottom):not(.bp3-position-left):not(
    .bp3-position-right):not(.bp3-vertical).bp3-overlay-appear{
      -webkit-transform:translateX(100%);
              transform:translateX(100%); }
    .bp3-drawer:not(.bp3-position-top):not(.bp3-position-bottom):not(.bp3-position-left):not(
    .bp3-position-right):not(.bp3-vertical).bp3-overlay-enter-active, .bp3-drawer:not(.bp3-position-top):not(.bp3-position-bottom):not(.bp3-position-left):not(
    .bp3-position-right):not(.bp3-vertical).bp3-overlay-appear-active{
      -webkit-transform:translateX(0);
              transform:translateX(0);
      -webkit-transition-delay:0;
              transition-delay:0;
      -webkit-transition-duration:200ms;
              transition-duration:200ms;
      -webkit-transition-property:-webkit-transform;
      transition-property:-webkit-transform;
      transition-property:transform;
      transition-property:transform, -webkit-transform;
      -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
              transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9); }
    .bp3-drawer:not(.bp3-position-top):not(.bp3-position-bottom):not(.bp3-position-left):not(
    .bp3-position-right):not(.bp3-vertical).bp3-overlay-exit{
      -webkit-transform:translateX(0);
              transform:translateX(0); }
    .bp3-drawer:not(.bp3-position-top):not(.bp3-position-bottom):not(.bp3-position-left):not(
    .bp3-position-right):not(.bp3-vertical).bp3-overlay-exit-active{
      -webkit-transform:translateX(100%);
              transform:translateX(100%);
      -webkit-transition-delay:0;
              transition-delay:0;
      -webkit-transition-duration:100ms;
              transition-duration:100ms;
      -webkit-transition-property:-webkit-transform;
      transition-property:-webkit-transform;
      transition-property:transform;
      transition-property:transform, -webkit-transform;
      -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
              transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9); }
  .bp3-drawer:not(.bp3-position-top):not(.bp3-position-bottom):not(.bp3-position-left):not(
  .bp3-position-right).bp3-vertical{
    bottom:0;
    height:50%;
    left:0;
    right:0; }
    .bp3-drawer:not(.bp3-position-top):not(.bp3-position-bottom):not(.bp3-position-left):not(
    .bp3-position-right).bp3-vertical.bp3-overlay-enter, .bp3-drawer:not(.bp3-position-top):not(.bp3-position-bottom):not(.bp3-position-left):not(
    .bp3-position-right).bp3-vertical.bp3-overlay-appear{
      -webkit-transform:translateY(100%);
              transform:translateY(100%); }
    .bp3-drawer:not(.bp3-position-top):not(.bp3-position-bottom):not(.bp3-position-left):not(
    .bp3-position-right).bp3-vertical.bp3-overlay-enter-active, .bp3-drawer:not(.bp3-position-top):not(.bp3-position-bottom):not(.bp3-position-left):not(
    .bp3-position-right).bp3-vertical.bp3-overlay-appear-active{
      -webkit-transform:translateY(0);
              transform:translateY(0);
      -webkit-transition-delay:0;
              transition-delay:0;
      -webkit-transition-duration:200ms;
              transition-duration:200ms;
      -webkit-transition-property:-webkit-transform;
      transition-property:-webkit-transform;
      transition-property:transform;
      transition-property:transform, -webkit-transform;
      -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
              transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9); }
    .bp3-drawer:not(.bp3-position-top):not(.bp3-position-bottom):not(.bp3-position-left):not(
    .bp3-position-right).bp3-vertical.bp3-overlay-exit{
      -webkit-transform:translateY(0);
              transform:translateY(0); }
    .bp3-drawer:not(.bp3-position-top):not(.bp3-position-bottom):not(.bp3-position-left):not(
    .bp3-position-right).bp3-vertical.bp3-overlay-exit-active{
      -webkit-transform:translateY(100%);
              transform:translateY(100%);
      -webkit-transition-delay:0;
              transition-delay:0;
      -webkit-transition-duration:100ms;
              transition-duration:100ms;
      -webkit-transition-property:-webkit-transform;
      transition-property:-webkit-transform;
      transition-property:transform;
      transition-property:transform, -webkit-transform;
      -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
              transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9); }
  .bp3-drawer.bp3-dark,
  .bp3-dark .bp3-drawer{
    background:#30404d;
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 4px 8px rgba(16, 22, 26, 0.4), 0 18px 46px 6px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 4px 8px rgba(16, 22, 26, 0.4), 0 18px 46px 6px rgba(16, 22, 26, 0.4);
    color:#f5f8fa; }

.bp3-drawer-header{
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center;
  border-radius:0;
  -webkit-box-shadow:0 1px 0 rgba(16, 22, 26, 0.15);
          box-shadow:0 1px 0 rgba(16, 22, 26, 0.15);
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-flex:0;
      -ms-flex:0 0 auto;
          flex:0 0 auto;
  min-height:40px;
  padding:5px;
  padding-left:20px;
  position:relative; }
  .bp3-drawer-header .bp3-icon-large,
  .bp3-drawer-header .bp3-icon{
    color:#5c7080;
    -webkit-box-flex:0;
        -ms-flex:0 0 auto;
            flex:0 0 auto;
    margin-right:10px; }
  .bp3-drawer-header .bp3-heading{
    overflow:hidden;
    text-overflow:ellipsis;
    white-space:nowrap;
    word-wrap:normal;
    -webkit-box-flex:1;
        -ms-flex:1 1 auto;
            flex:1 1 auto;
    line-height:inherit;
    margin:0; }
    .bp3-drawer-header .bp3-heading:last-child{
      margin-right:20px; }
  .bp3-dark .bp3-drawer-header{
    -webkit-box-shadow:0 1px 0 rgba(16, 22, 26, 0.4);
            box-shadow:0 1px 0 rgba(16, 22, 26, 0.4); }
    .bp3-dark .bp3-drawer-header .bp3-icon-large,
    .bp3-dark .bp3-drawer-header .bp3-icon{
      color:#a7b6c2; }

.bp3-drawer-body{
  -webkit-box-flex:1;
      -ms-flex:1 1 auto;
          flex:1 1 auto;
  line-height:18px;
  overflow:auto; }

.bp3-drawer-footer{
  -webkit-box-shadow:inset 0 1px 0 rgba(16, 22, 26, 0.15);
          box-shadow:inset 0 1px 0 rgba(16, 22, 26, 0.15);
  -webkit-box-flex:0;
      -ms-flex:0 0 auto;
          flex:0 0 auto;
  padding:10px 20px;
  position:relative; }
  .bp3-dark .bp3-drawer-footer{
    -webkit-box-shadow:inset 0 1px 0 rgba(16, 22, 26, 0.4);
            box-shadow:inset 0 1px 0 rgba(16, 22, 26, 0.4); }
.bp3-editable-text{
  cursor:text;
  display:inline-block;
  max-width:100%;
  position:relative;
  vertical-align:top;
  white-space:nowrap; }
  .bp3-editable-text::before{
    bottom:-3px;
    left:-3px;
    position:absolute;
    right:-3px;
    top:-3px;
    border-radius:3px;
    content:"";
    -webkit-transition:background-color 100ms cubic-bezier(0.4, 1, 0.75, 0.9), -webkit-box-shadow 100ms cubic-bezier(0.4, 1, 0.75, 0.9);
    transition:background-color 100ms cubic-bezier(0.4, 1, 0.75, 0.9), -webkit-box-shadow 100ms cubic-bezier(0.4, 1, 0.75, 0.9);
    transition:background-color 100ms cubic-bezier(0.4, 1, 0.75, 0.9), box-shadow 100ms cubic-bezier(0.4, 1, 0.75, 0.9);
    transition:background-color 100ms cubic-bezier(0.4, 1, 0.75, 0.9), box-shadow 100ms cubic-bezier(0.4, 1, 0.75, 0.9), -webkit-box-shadow 100ms cubic-bezier(0.4, 1, 0.75, 0.9); }
  .bp3-editable-text:hover::before{
    -webkit-box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px rgba(16, 22, 26, 0.15);
            box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px rgba(16, 22, 26, 0.15); }
  .bp3-editable-text.bp3-editable-text-editing::before{
    background-color:#ffffff;
    -webkit-box-shadow:0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
  .bp3-editable-text.bp3-disabled::before{
    -webkit-box-shadow:none;
            box-shadow:none; }
  .bp3-editable-text.bp3-intent-primary .bp3-editable-text-input,
  .bp3-editable-text.bp3-intent-primary .bp3-editable-text-content{
    color:#137cbd; }
  .bp3-editable-text.bp3-intent-primary:hover::before{
    -webkit-box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px rgba(19, 124, 189, 0.4);
            box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px rgba(19, 124, 189, 0.4); }
  .bp3-editable-text.bp3-intent-primary.bp3-editable-text-editing::before{
    -webkit-box-shadow:0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
  .bp3-editable-text.bp3-intent-success .bp3-editable-text-input,
  .bp3-editable-text.bp3-intent-success .bp3-editable-text-content{
    color:#0f9960; }
  .bp3-editable-text.bp3-intent-success:hover::before{
    -webkit-box-shadow:0 0 0 0 rgba(15, 153, 96, 0), 0 0 0 0 rgba(15, 153, 96, 0), inset 0 0 0 1px rgba(15, 153, 96, 0.4);
            box-shadow:0 0 0 0 rgba(15, 153, 96, 0), 0 0 0 0 rgba(15, 153, 96, 0), inset 0 0 0 1px rgba(15, 153, 96, 0.4); }
  .bp3-editable-text.bp3-intent-success.bp3-editable-text-editing::before{
    -webkit-box-shadow:0 0 0 1px #0f9960, 0 0 0 3px rgba(15, 153, 96, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 1px #0f9960, 0 0 0 3px rgba(15, 153, 96, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
  .bp3-editable-text.bp3-intent-warning .bp3-editable-text-input,
  .bp3-editable-text.bp3-intent-warning .bp3-editable-text-content{
    color:#d9822b; }
  .bp3-editable-text.bp3-intent-warning:hover::before{
    -webkit-box-shadow:0 0 0 0 rgba(217, 130, 43, 0), 0 0 0 0 rgba(217, 130, 43, 0), inset 0 0 0 1px rgba(217, 130, 43, 0.4);
            box-shadow:0 0 0 0 rgba(217, 130, 43, 0), 0 0 0 0 rgba(217, 130, 43, 0), inset 0 0 0 1px rgba(217, 130, 43, 0.4); }
  .bp3-editable-text.bp3-intent-warning.bp3-editable-text-editing::before{
    -webkit-box-shadow:0 0 0 1px #d9822b, 0 0 0 3px rgba(217, 130, 43, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 1px #d9822b, 0 0 0 3px rgba(217, 130, 43, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
  .bp3-editable-text.bp3-intent-danger .bp3-editable-text-input,
  .bp3-editable-text.bp3-intent-danger .bp3-editable-text-content{
    color:#db3737; }
  .bp3-editable-text.bp3-intent-danger:hover::before{
    -webkit-box-shadow:0 0 0 0 rgba(219, 55, 55, 0), 0 0 0 0 rgba(219, 55, 55, 0), inset 0 0 0 1px rgba(219, 55, 55, 0.4);
            box-shadow:0 0 0 0 rgba(219, 55, 55, 0), 0 0 0 0 rgba(219, 55, 55, 0), inset 0 0 0 1px rgba(219, 55, 55, 0.4); }
  .bp3-editable-text.bp3-intent-danger.bp3-editable-text-editing::before{
    -webkit-box-shadow:0 0 0 1px #db3737, 0 0 0 3px rgba(219, 55, 55, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 1px #db3737, 0 0 0 3px rgba(219, 55, 55, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
  .bp3-dark .bp3-editable-text:hover::before{
    -webkit-box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px rgba(255, 255, 255, 0.15);
            box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px rgba(255, 255, 255, 0.15); }
  .bp3-dark .bp3-editable-text.bp3-editable-text-editing::before{
    background-color:rgba(16, 22, 26, 0.3);
    -webkit-box-shadow:0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
  .bp3-dark .bp3-editable-text.bp3-disabled::before{
    -webkit-box-shadow:none;
            box-shadow:none; }
  .bp3-dark .bp3-editable-text.bp3-intent-primary .bp3-editable-text-content{
    color:#48aff0; }
  .bp3-dark .bp3-editable-text.bp3-intent-primary:hover::before{
    -webkit-box-shadow:0 0 0 0 rgba(72, 175, 240, 0), 0 0 0 0 rgba(72, 175, 240, 0), inset 0 0 0 1px rgba(72, 175, 240, 0.4);
            box-shadow:0 0 0 0 rgba(72, 175, 240, 0), 0 0 0 0 rgba(72, 175, 240, 0), inset 0 0 0 1px rgba(72, 175, 240, 0.4); }
  .bp3-dark .bp3-editable-text.bp3-intent-primary.bp3-editable-text-editing::before{
    -webkit-box-shadow:0 0 0 1px #48aff0, 0 0 0 3px rgba(72, 175, 240, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px #48aff0, 0 0 0 3px rgba(72, 175, 240, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
  .bp3-dark .bp3-editable-text.bp3-intent-success .bp3-editable-text-content{
    color:#3dcc91; }
  .bp3-dark .bp3-editable-text.bp3-intent-success:hover::before{
    -webkit-box-shadow:0 0 0 0 rgba(61, 204, 145, 0), 0 0 0 0 rgba(61, 204, 145, 0), inset 0 0 0 1px rgba(61, 204, 145, 0.4);
            box-shadow:0 0 0 0 rgba(61, 204, 145, 0), 0 0 0 0 rgba(61, 204, 145, 0), inset 0 0 0 1px rgba(61, 204, 145, 0.4); }
  .bp3-dark .bp3-editable-text.bp3-intent-success.bp3-editable-text-editing::before{
    -webkit-box-shadow:0 0 0 1px #3dcc91, 0 0 0 3px rgba(61, 204, 145, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px #3dcc91, 0 0 0 3px rgba(61, 204, 145, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
  .bp3-dark .bp3-editable-text.bp3-intent-warning .bp3-editable-text-content{
    color:#ffb366; }
  .bp3-dark .bp3-editable-text.bp3-intent-warning:hover::before{
    -webkit-box-shadow:0 0 0 0 rgba(255, 179, 102, 0), 0 0 0 0 rgba(255, 179, 102, 0), inset 0 0 0 1px rgba(255, 179, 102, 0.4);
            box-shadow:0 0 0 0 rgba(255, 179, 102, 0), 0 0 0 0 rgba(255, 179, 102, 0), inset 0 0 0 1px rgba(255, 179, 102, 0.4); }
  .bp3-dark .bp3-editable-text.bp3-intent-warning.bp3-editable-text-editing::before{
    -webkit-box-shadow:0 0 0 1px #ffb366, 0 0 0 3px rgba(255, 179, 102, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px #ffb366, 0 0 0 3px rgba(255, 179, 102, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
  .bp3-dark .bp3-editable-text.bp3-intent-danger .bp3-editable-text-content{
    color:#ff7373; }
  .bp3-dark .bp3-editable-text.bp3-intent-danger:hover::before{
    -webkit-box-shadow:0 0 0 0 rgba(255, 115, 115, 0), 0 0 0 0 rgba(255, 115, 115, 0), inset 0 0 0 1px rgba(255, 115, 115, 0.4);
            box-shadow:0 0 0 0 rgba(255, 115, 115, 0), 0 0 0 0 rgba(255, 115, 115, 0), inset 0 0 0 1px rgba(255, 115, 115, 0.4); }
  .bp3-dark .bp3-editable-text.bp3-intent-danger.bp3-editable-text-editing::before{
    -webkit-box-shadow:0 0 0 1px #ff7373, 0 0 0 3px rgba(255, 115, 115, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px #ff7373, 0 0 0 3px rgba(255, 115, 115, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }

.bp3-editable-text-input,
.bp3-editable-text-content{
  color:inherit;
  display:inherit;
  font:inherit;
  letter-spacing:inherit;
  max-width:inherit;
  min-width:inherit;
  position:relative;
  resize:none;
  text-transform:inherit;
  vertical-align:top; }

.bp3-editable-text-input{
  background:none;
  border:none;
  -webkit-box-shadow:none;
          box-shadow:none;
  padding:0;
  white-space:pre-wrap;
  width:100%; }
  .bp3-editable-text-input::-webkit-input-placeholder{
    color:rgba(92, 112, 128, 0.6);
    opacity:1; }
  .bp3-editable-text-input::-moz-placeholder{
    color:rgba(92, 112, 128, 0.6);
    opacity:1; }
  .bp3-editable-text-input:-ms-input-placeholder{
    color:rgba(92, 112, 128, 0.6);
    opacity:1; }
  .bp3-editable-text-input::-ms-input-placeholder{
    color:rgba(92, 112, 128, 0.6);
    opacity:1; }
  .bp3-editable-text-input::placeholder{
    color:rgba(92, 112, 128, 0.6);
    opacity:1; }
  .bp3-editable-text-input:focus{
    outline:none; }
  .bp3-editable-text-input::-ms-clear{
    display:none; }

.bp3-editable-text-content{
  overflow:hidden;
  padding-right:2px;
  text-overflow:ellipsis;
  white-space:pre; }
  .bp3-editable-text-editing > .bp3-editable-text-content{
    left:0;
    position:absolute;
    visibility:hidden; }
  .bp3-editable-text-placeholder > .bp3-editable-text-content{
    color:rgba(92, 112, 128, 0.6); }
    .bp3-dark .bp3-editable-text-placeholder > .bp3-editable-text-content{
      color:rgba(167, 182, 194, 0.6); }

.bp3-editable-text.bp3-multiline{
  display:block; }
  .bp3-editable-text.bp3-multiline .bp3-editable-text-content{
    overflow:auto;
    white-space:pre-wrap;
    word-wrap:break-word; }
.bp3-divider{
  border-bottom:1px solid rgba(16, 22, 26, 0.15);
  border-right:1px solid rgba(16, 22, 26, 0.15);
  margin:5px; }
  .bp3-dark .bp3-divider{
    border-color:rgba(16, 22, 26, 0.4); }
.bp3-control-group{
  -webkit-transform:translateZ(0);
          transform:translateZ(0);
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-orient:horizontal;
  -webkit-box-direction:normal;
      -ms-flex-direction:row;
          flex-direction:row;
  -webkit-box-align:stretch;
      -ms-flex-align:stretch;
          align-items:stretch; }
  .bp3-control-group > *{
    -webkit-box-flex:0;
        -ms-flex-positive:0;
            flex-grow:0;
    -ms-flex-negative:0;
        flex-shrink:0; }
  .bp3-control-group > .bp3-fill{
    -webkit-box-flex:1;
        -ms-flex-positive:1;
            flex-grow:1;
    -ms-flex-negative:1;
        flex-shrink:1; }
  .bp3-control-group .bp3-button,
  .bp3-control-group .bp3-html-select,
  .bp3-control-group .bp3-input,
  .bp3-control-group .bp3-select{
    position:relative; }
  .bp3-control-group .bp3-input{
    border-radius:inherit;
    z-index:2; }
    .bp3-control-group .bp3-input:focus{
      border-radius:3px;
      z-index:14; }
    .bp3-control-group .bp3-input[class*="bp3-intent"]{
      z-index:13; }
      .bp3-control-group .bp3-input[class*="bp3-intent"]:focus{
        z-index:15; }
    .bp3-control-group .bp3-input[readonly], .bp3-control-group .bp3-input:disabled, .bp3-control-group .bp3-input.bp3-disabled{
      z-index:1; }
  .bp3-control-group .bp3-input-group[class*="bp3-intent"] .bp3-input{
    z-index:13; }
    .bp3-control-group .bp3-input-group[class*="bp3-intent"] .bp3-input:focus{
      z-index:15; }
  .bp3-control-group .bp3-button,
  .bp3-control-group .bp3-html-select select,
  .bp3-control-group .bp3-select select{
    -webkit-transform:translateZ(0);
            transform:translateZ(0);
    border-radius:inherit;
    z-index:4; }
    .bp3-control-group .bp3-button:focus,
    .bp3-control-group .bp3-html-select select:focus,
    .bp3-control-group .bp3-select select:focus{
      z-index:5; }
    .bp3-control-group .bp3-button:hover,
    .bp3-control-group .bp3-html-select select:hover,
    .bp3-control-group .bp3-select select:hover{
      z-index:6; }
    .bp3-control-group .bp3-button:active,
    .bp3-control-group .bp3-html-select select:active,
    .bp3-control-group .bp3-select select:active{
      z-index:7; }
    .bp3-control-group .bp3-button[readonly], .bp3-control-group .bp3-button:disabled, .bp3-control-group .bp3-button.bp3-disabled,
    .bp3-control-group .bp3-html-select select[readonly],
    .bp3-control-group .bp3-html-select select:disabled,
    .bp3-control-group .bp3-html-select select.bp3-disabled,
    .bp3-control-group .bp3-select select[readonly],
    .bp3-control-group .bp3-select select:disabled,
    .bp3-control-group .bp3-select select.bp3-disabled{
      z-index:3; }
    .bp3-control-group .bp3-button[class*="bp3-intent"],
    .bp3-control-group .bp3-html-select select[class*="bp3-intent"],
    .bp3-control-group .bp3-select select[class*="bp3-intent"]{
      z-index:9; }
      .bp3-control-group .bp3-button[class*="bp3-intent"]:focus,
      .bp3-control-group .bp3-html-select select[class*="bp3-intent"]:focus,
      .bp3-control-group .bp3-select select[class*="bp3-intent"]:focus{
        z-index:10; }
      .bp3-control-group .bp3-button[class*="bp3-intent"]:hover,
      .bp3-control-group .bp3-html-select select[class*="bp3-intent"]:hover,
      .bp3-control-group .bp3-select select[class*="bp3-intent"]:hover{
        z-index:11; }
      .bp3-control-group .bp3-button[class*="bp3-intent"]:active,
      .bp3-control-group .bp3-html-select select[class*="bp3-intent"]:active,
      .bp3-control-group .bp3-select select[class*="bp3-intent"]:active{
        z-index:12; }
      .bp3-control-group .bp3-button[class*="bp3-intent"][readonly], .bp3-control-group .bp3-button[class*="bp3-intent"]:disabled, .bp3-control-group .bp3-button[class*="bp3-intent"].bp3-disabled,
      .bp3-control-group .bp3-html-select select[class*="bp3-intent"][readonly],
      .bp3-control-group .bp3-html-select select[class*="bp3-intent"]:disabled,
      .bp3-control-group .bp3-html-select select[class*="bp3-intent"].bp3-disabled,
      .bp3-control-group .bp3-select select[class*="bp3-intent"][readonly],
      .bp3-control-group .bp3-select select[class*="bp3-intent"]:disabled,
      .bp3-control-group .bp3-select select[class*="bp3-intent"].bp3-disabled{
        z-index:8; }
  .bp3-control-group .bp3-input-group > .bp3-icon,
  .bp3-control-group .bp3-input-group > .bp3-button,
  .bp3-control-group .bp3-input-group > .bp3-input-left-container,
  .bp3-control-group .bp3-input-group > .bp3-input-action{
    z-index:16; }
  .bp3-control-group .bp3-select::after,
  .bp3-control-group .bp3-html-select::after,
  .bp3-control-group .bp3-select > .bp3-icon,
  .bp3-control-group .bp3-html-select > .bp3-icon{
    z-index:17; }
  .bp3-control-group .bp3-select:focus-within{
    z-index:5; }
  .bp3-control-group:not(.bp3-vertical) > *:not(.bp3-divider){
    margin-right:-1px; }
  .bp3-control-group:not(.bp3-vertical) > .bp3-divider:not(:first-child){
    margin-left:6px; }
  .bp3-dark .bp3-control-group:not(.bp3-vertical) > *:not(.bp3-divider){
    margin-right:0; }
  .bp3-dark .bp3-control-group:not(.bp3-vertical) > .bp3-button + .bp3-button{
    margin-left:1px; }
  .bp3-control-group .bp3-popover-wrapper,
  .bp3-control-group .bp3-popover-target{
    border-radius:inherit; }
  .bp3-control-group > :first-child{
    border-radius:3px 0 0 3px; }
  .bp3-control-group > :last-child{
    border-radius:0 3px 3px 0;
    margin-right:0; }
  .bp3-control-group > :only-child{
    border-radius:3px;
    margin-right:0; }
  .bp3-control-group .bp3-input-group .bp3-button{
    border-radius:3px; }
  .bp3-control-group .bp3-numeric-input:not(:first-child) .bp3-input-group{
    border-bottom-left-radius:0;
    border-top-left-radius:0; }
  .bp3-control-group.bp3-fill{
    width:100%; }
  .bp3-control-group > .bp3-fill{
    -webkit-box-flex:1;
        -ms-flex:1 1 auto;
            flex:1 1 auto; }
  .bp3-control-group.bp3-fill > *:not(.bp3-fixed){
    -webkit-box-flex:1;
        -ms-flex:1 1 auto;
            flex:1 1 auto; }
  .bp3-control-group.bp3-vertical{
    -webkit-box-orient:vertical;
    -webkit-box-direction:normal;
        -ms-flex-direction:column;
            flex-direction:column; }
    .bp3-control-group.bp3-vertical > *{
      margin-top:-1px; }
    .bp3-control-group.bp3-vertical > :first-child{
      border-radius:3px 3px 0 0;
      margin-top:0; }
    .bp3-control-group.bp3-vertical > :last-child{
      border-radius:0 0 3px 3px; }
.bp3-control{
  cursor:pointer;
  display:block;
  margin-bottom:10px;
  position:relative;
  text-transform:none; }
  .bp3-control input:checked ~ .bp3-control-indicator{
    background-color:#137cbd;
    background-image:-webkit-gradient(linear, left top, left bottom, from(rgba(255, 255, 255, 0.1)), to(rgba(255, 255, 255, 0)));
    background-image:linear-gradient(to bottom, rgba(255, 255, 255, 0.1), rgba(255, 255, 255, 0));
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
    color:#ffffff; }
  .bp3-control:hover input:checked ~ .bp3-control-indicator{
    background-color:#106ba3;
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2); }
  .bp3-control input:not(:disabled):active:checked ~ .bp3-control-indicator{
    background:#0e5a8a;
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2); }
  .bp3-control input:disabled:checked ~ .bp3-control-indicator{
    background:rgba(19, 124, 189, 0.5);
    -webkit-box-shadow:none;
            box-shadow:none; }
  .bp3-dark .bp3-control input:checked ~ .bp3-control-indicator{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4); }
  .bp3-dark .bp3-control:hover input:checked ~ .bp3-control-indicator{
    background-color:#106ba3;
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4); }
  .bp3-dark .bp3-control input:not(:disabled):active:checked ~ .bp3-control-indicator{
    background-color:#0e5a8a;
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2); }
  .bp3-dark .bp3-control input:disabled:checked ~ .bp3-control-indicator{
    background:rgba(14, 90, 138, 0.5);
    -webkit-box-shadow:none;
            box-shadow:none; }
  .bp3-control:not(.bp3-align-right){
    padding-left:26px; }
    .bp3-control:not(.bp3-align-right) .bp3-control-indicator{
      margin-left:-26px; }
  .bp3-control.bp3-align-right{
    padding-right:26px; }
    .bp3-control.bp3-align-right .bp3-control-indicator{
      margin-right:-26px; }
  .bp3-control.bp3-disabled{
    color:rgba(92, 112, 128, 0.6);
    cursor:not-allowed; }
  .bp3-control.bp3-inline{
    display:inline-block;
    margin-right:20px; }
  .bp3-control input{
    left:0;
    opacity:0;
    position:absolute;
    top:0;
    z-index:-1; }
  .bp3-control .bp3-control-indicator{
    background-clip:padding-box;
    background-color:#f5f8fa;
    background-image:-webkit-gradient(linear, left top, left bottom, from(rgba(255, 255, 255, 0.8)), to(rgba(255, 255, 255, 0)));
    background-image:linear-gradient(to bottom, rgba(255, 255, 255, 0.8), rgba(255, 255, 255, 0));
    border:none;
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
    cursor:pointer;
    display:inline-block;
    font-size:16px;
    height:1em;
    margin-right:10px;
    margin-top:-3px;
    position:relative;
    -webkit-user-select:none;
       -moz-user-select:none;
        -ms-user-select:none;
            user-select:none;
    vertical-align:middle;
    width:1em; }
    .bp3-control .bp3-control-indicator::before{
      content:"";
      display:block;
      height:1em;
      width:1em; }
  .bp3-control:hover .bp3-control-indicator{
    background-color:#ebf1f5; }
  .bp3-control input:not(:disabled):active ~ .bp3-control-indicator{
    background:#d8e1e8;
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 1px 2px rgba(16, 22, 26, 0.2);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 1px 2px rgba(16, 22, 26, 0.2); }
  .bp3-control input:disabled ~ .bp3-control-indicator{
    background:rgba(206, 217, 224, 0.5);
    -webkit-box-shadow:none;
            box-shadow:none;
    cursor:not-allowed; }
  .bp3-control input:focus ~ .bp3-control-indicator{
    outline:rgba(19, 124, 189, 0.6) auto 2px;
    outline-offset:2px;
    -moz-outline-radius:6px; }
  .bp3-control.bp3-align-right .bp3-control-indicator{
    float:right;
    margin-left:10px;
    margin-top:1px; }
  .bp3-control.bp3-large{
    font-size:16px; }
    .bp3-control.bp3-large:not(.bp3-align-right){
      padding-left:30px; }
      .bp3-control.bp3-large:not(.bp3-align-right) .bp3-control-indicator{
        margin-left:-30px; }
    .bp3-control.bp3-large.bp3-align-right{
      padding-right:30px; }
      .bp3-control.bp3-large.bp3-align-right .bp3-control-indicator{
        margin-right:-30px; }
    .bp3-control.bp3-large .bp3-control-indicator{
      font-size:20px; }
    .bp3-control.bp3-large.bp3-align-right .bp3-control-indicator{
      margin-top:0; }
  .bp3-control.bp3-checkbox input:indeterminate ~ .bp3-control-indicator{
    background-color:#137cbd;
    background-image:-webkit-gradient(linear, left top, left bottom, from(rgba(255, 255, 255, 0.1)), to(rgba(255, 255, 255, 0)));
    background-image:linear-gradient(to bottom, rgba(255, 255, 255, 0.1), rgba(255, 255, 255, 0));
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
    color:#ffffff; }
  .bp3-control.bp3-checkbox:hover input:indeterminate ~ .bp3-control-indicator{
    background-color:#106ba3;
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 -1px 0 rgba(16, 22, 26, 0.2); }
  .bp3-control.bp3-checkbox input:not(:disabled):active:indeterminate ~ .bp3-control-indicator{
    background:#0e5a8a;
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2); }
  .bp3-control.bp3-checkbox input:disabled:indeterminate ~ .bp3-control-indicator{
    background:rgba(19, 124, 189, 0.5);
    -webkit-box-shadow:none;
            box-shadow:none; }
  .bp3-dark .bp3-control.bp3-checkbox input:indeterminate ~ .bp3-control-indicator{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4); }
  .bp3-dark .bp3-control.bp3-checkbox:hover input:indeterminate ~ .bp3-control-indicator{
    background-color:#106ba3;
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4); }
  .bp3-dark .bp3-control.bp3-checkbox input:not(:disabled):active:indeterminate ~ .bp3-control-indicator{
    background-color:#0e5a8a;
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4), inset 0 1px 2px rgba(16, 22, 26, 0.2); }
  .bp3-dark .bp3-control.bp3-checkbox input:disabled:indeterminate ~ .bp3-control-indicator{
    background:rgba(14, 90, 138, 0.5);
    -webkit-box-shadow:none;
            box-shadow:none; }
  .bp3-control.bp3-checkbox .bp3-control-indicator{
    border-radius:3px; }
  .bp3-control.bp3-checkbox input:checked ~ .bp3-control-indicator::before{
    background-image:url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 16 16'%3e%3cpath fill-rule='evenodd' clip-rule='evenodd' d='M12 5c-.28 0-.53.11-.71.29L7 9.59l-2.29-2.3a1.003 1.003 0 00-1.42 1.42l3 3c.18.18.43.29.71.29s.53-.11.71-.29l5-5A1.003 1.003 0 0012 5z' fill='white'/%3e%3c/svg%3e"); }
  .bp3-control.bp3-checkbox input:indeterminate ~ .bp3-control-indicator::before{
    background-image:url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 16 16'%3e%3cpath fill-rule='evenodd' clip-rule='evenodd' d='M11 7H5c-.55 0-1 .45-1 1s.45 1 1 1h6c.55 0 1-.45 1-1s-.45-1-1-1z' fill='white'/%3e%3c/svg%3e"); }
  .bp3-control.bp3-radio .bp3-control-indicator{
    border-radius:50%; }
  .bp3-control.bp3-radio input:checked ~ .bp3-control-indicator::before{
    background-image:radial-gradient(#ffffff, #ffffff 28%, transparent 32%); }
  .bp3-control.bp3-radio input:checked:disabled ~ .bp3-control-indicator::before{
    opacity:0.5; }
  .bp3-control.bp3-radio input:focus ~ .bp3-control-indicator{
    -moz-outline-radius:16px; }
  .bp3-control.bp3-switch input ~ .bp3-control-indicator{
    background:rgba(167, 182, 194, 0.5); }
  .bp3-control.bp3-switch:hover input ~ .bp3-control-indicator{
    background:rgba(115, 134, 148, 0.5); }
  .bp3-control.bp3-switch input:not(:disabled):active ~ .bp3-control-indicator{
    background:rgba(92, 112, 128, 0.5); }
  .bp3-control.bp3-switch input:disabled ~ .bp3-control-indicator{
    background:rgba(206, 217, 224, 0.5); }
    .bp3-control.bp3-switch input:disabled ~ .bp3-control-indicator::before{
      background:rgba(255, 255, 255, 0.8); }
  .bp3-control.bp3-switch input:checked ~ .bp3-control-indicator{
    background:#137cbd; }
  .bp3-control.bp3-switch:hover input:checked ~ .bp3-control-indicator{
    background:#106ba3; }
  .bp3-control.bp3-switch input:checked:not(:disabled):active ~ .bp3-control-indicator{
    background:#0e5a8a; }
  .bp3-control.bp3-switch input:checked:disabled ~ .bp3-control-indicator{
    background:rgba(19, 124, 189, 0.5); }
    .bp3-control.bp3-switch input:checked:disabled ~ .bp3-control-indicator::before{
      background:rgba(255, 255, 255, 0.8); }
  .bp3-control.bp3-switch:not(.bp3-align-right){
    padding-left:38px; }
    .bp3-control.bp3-switch:not(.bp3-align-right) .bp3-control-indicator{
      margin-left:-38px; }
  .bp3-control.bp3-switch.bp3-align-right{
    padding-right:38px; }
    .bp3-control.bp3-switch.bp3-align-right .bp3-control-indicator{
      margin-right:-38px; }
  .bp3-control.bp3-switch .bp3-control-indicator{
    border:none;
    border-radius:1.75em;
    -webkit-box-shadow:none !important;
            box-shadow:none !important;
    min-width:1.75em;
    -webkit-transition:background-color 100ms cubic-bezier(0.4, 1, 0.75, 0.9);
    transition:background-color 100ms cubic-bezier(0.4, 1, 0.75, 0.9);
    width:auto; }
    .bp3-control.bp3-switch .bp3-control-indicator::before{
      background:#ffffff;
      border-radius:50%;
      -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 1px 1px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 1px 1px rgba(16, 22, 26, 0.2);
      height:calc(1em - 4px);
      left:0;
      margin:2px;
      position:absolute;
      -webkit-transition:left 100ms cubic-bezier(0.4, 1, 0.75, 0.9);
      transition:left 100ms cubic-bezier(0.4, 1, 0.75, 0.9);
      width:calc(1em - 4px); }
  .bp3-control.bp3-switch input:checked ~ .bp3-control-indicator::before{
    left:calc(100% - 1em); }
  .bp3-control.bp3-switch.bp3-large:not(.bp3-align-right){
    padding-left:45px; }
    .bp3-control.bp3-switch.bp3-large:not(.bp3-align-right) .bp3-control-indicator{
      margin-left:-45px; }
  .bp3-control.bp3-switch.bp3-large.bp3-align-right{
    padding-right:45px; }
    .bp3-control.bp3-switch.bp3-large.bp3-align-right .bp3-control-indicator{
      margin-right:-45px; }
  .bp3-dark .bp3-control.bp3-switch input ~ .bp3-control-indicator{
    background:rgba(16, 22, 26, 0.5); }
  .bp3-dark .bp3-control.bp3-switch:hover input ~ .bp3-control-indicator{
    background:rgba(16, 22, 26, 0.7); }
  .bp3-dark .bp3-control.bp3-switch input:not(:disabled):active ~ .bp3-control-indicator{
    background:rgba(16, 22, 26, 0.9); }
  .bp3-dark .bp3-control.bp3-switch input:disabled ~ .bp3-control-indicator{
    background:rgba(57, 75, 89, 0.5); }
    .bp3-dark .bp3-control.bp3-switch input:disabled ~ .bp3-control-indicator::before{
      background:rgba(16, 22, 26, 0.4); }
  .bp3-dark .bp3-control.bp3-switch input:checked ~ .bp3-control-indicator{
    background:#137cbd; }
  .bp3-dark .bp3-control.bp3-switch:hover input:checked ~ .bp3-control-indicator{
    background:#106ba3; }
  .bp3-dark .bp3-control.bp3-switch input:checked:not(:disabled):active ~ .bp3-control-indicator{
    background:#0e5a8a; }
  .bp3-dark .bp3-control.bp3-switch input:checked:disabled ~ .bp3-control-indicator{
    background:rgba(14, 90, 138, 0.5); }
    .bp3-dark .bp3-control.bp3-switch input:checked:disabled ~ .bp3-control-indicator::before{
      background:rgba(16, 22, 26, 0.4); }
  .bp3-dark .bp3-control.bp3-switch .bp3-control-indicator::before{
    background:#394b59;
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4); }
  .bp3-dark .bp3-control.bp3-switch input:checked ~ .bp3-control-indicator::before{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4); }
  .bp3-control.bp3-switch .bp3-switch-inner-text{
    font-size:0.7em;
    text-align:center; }
  .bp3-control.bp3-switch .bp3-control-indicator-child:first-child{
    line-height:0;
    margin-left:0.5em;
    margin-right:1.2em;
    visibility:hidden; }
  .bp3-control.bp3-switch .bp3-control-indicator-child:last-child{
    line-height:1em;
    margin-left:1.2em;
    margin-right:0.5em;
    visibility:visible; }
  .bp3-control.bp3-switch input:checked ~ .bp3-control-indicator .bp3-control-indicator-child:first-child{
    line-height:1em;
    visibility:visible; }
  .bp3-control.bp3-switch input:checked ~ .bp3-control-indicator .bp3-control-indicator-child:last-child{
    line-height:0;
    visibility:hidden; }
  .bp3-dark .bp3-control{
    color:#f5f8fa; }
    .bp3-dark .bp3-control.bp3-disabled{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-control .bp3-control-indicator{
      background-color:#394b59;
      background-image:-webkit-gradient(linear, left top, left bottom, from(rgba(255, 255, 255, 0.05)), to(rgba(255, 255, 255, 0)));
      background-image:linear-gradient(to bottom, rgba(255, 255, 255, 0.05), rgba(255, 255, 255, 0));
      -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4); }
    .bp3-dark .bp3-control:hover .bp3-control-indicator{
      background-color:#30404d; }
    .bp3-dark .bp3-control input:not(:disabled):active ~ .bp3-control-indicator{
      background:#202b33;
      -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.6), inset 0 1px 2px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px rgba(16, 22, 26, 0.6), inset 0 1px 2px rgba(16, 22, 26, 0.2); }
    .bp3-dark .bp3-control input:disabled ~ .bp3-control-indicator{
      background:rgba(57, 75, 89, 0.5);
      -webkit-box-shadow:none;
              box-shadow:none;
      cursor:not-allowed; }
    .bp3-dark .bp3-control.bp3-checkbox input:disabled:checked ~ .bp3-control-indicator, .bp3-dark .bp3-control.bp3-checkbox input:disabled:indeterminate ~ .bp3-control-indicator{
      color:rgba(167, 182, 194, 0.6); }
.bp3-file-input{
  cursor:pointer;
  display:inline-block;
  height:30px;
  position:relative; }
  .bp3-file-input input{
    margin:0;
    min-width:200px;
    opacity:0; }
    .bp3-file-input input:disabled + .bp3-file-upload-input,
    .bp3-file-input input.bp3-disabled + .bp3-file-upload-input{
      background:rgba(206, 217, 224, 0.5);
      -webkit-box-shadow:none;
              box-shadow:none;
      color:rgba(92, 112, 128, 0.6);
      cursor:not-allowed;
      resize:none; }
      .bp3-file-input input:disabled + .bp3-file-upload-input::after,
      .bp3-file-input input.bp3-disabled + .bp3-file-upload-input::after{
        background-color:rgba(206, 217, 224, 0.5);
        background-image:none;
        -webkit-box-shadow:none;
                box-shadow:none;
        color:rgba(92, 112, 128, 0.6);
        cursor:not-allowed;
        outline:none; }
        .bp3-file-input input:disabled + .bp3-file-upload-input::after.bp3-active, .bp3-file-input input:disabled + .bp3-file-upload-input::after.bp3-active:hover,
        .bp3-file-input input.bp3-disabled + .bp3-file-upload-input::after.bp3-active,
        .bp3-file-input input.bp3-disabled + .bp3-file-upload-input::after.bp3-active:hover{
          background:rgba(206, 217, 224, 0.7); }
      .bp3-dark .bp3-file-input input:disabled + .bp3-file-upload-input, .bp3-dark
      .bp3-file-input input.bp3-disabled + .bp3-file-upload-input{
        background:rgba(57, 75, 89, 0.5);
        -webkit-box-shadow:none;
                box-shadow:none;
        color:rgba(167, 182, 194, 0.6); }
        .bp3-dark .bp3-file-input input:disabled + .bp3-file-upload-input::after, .bp3-dark
        .bp3-file-input input.bp3-disabled + .bp3-file-upload-input::after{
          background-color:rgba(57, 75, 89, 0.5);
          background-image:none;
          -webkit-box-shadow:none;
                  box-shadow:none;
          color:rgba(167, 182, 194, 0.6); }
          .bp3-dark .bp3-file-input input:disabled + .bp3-file-upload-input::after.bp3-active, .bp3-dark
          .bp3-file-input input.bp3-disabled + .bp3-file-upload-input::after.bp3-active{
            background:rgba(57, 75, 89, 0.7); }
  .bp3-file-input.bp3-file-input-has-selection .bp3-file-upload-input{
    color:#182026; }
  .bp3-dark .bp3-file-input.bp3-file-input-has-selection .bp3-file-upload-input{
    color:#f5f8fa; }
  .bp3-file-input.bp3-fill{
    width:100%; }
  .bp3-file-input.bp3-large,
  .bp3-large .bp3-file-input{
    height:40px; }
  .bp3-file-input .bp3-file-upload-input-custom-text::after{
    content:attr(bp3-button-text); }

.bp3-file-upload-input{
  -webkit-appearance:none;
     -moz-appearance:none;
          appearance:none;
  background:#ffffff;
  border:none;
  border-radius:3px;
  -webkit-box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2);
          box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2);
  color:#182026;
  font-size:14px;
  font-weight:400;
  height:30px;
  line-height:30px;
  outline:none;
  padding:0 10px;
  -webkit-transition:-webkit-box-shadow 100ms cubic-bezier(0.4, 1, 0.75, 0.9);
  transition:-webkit-box-shadow 100ms cubic-bezier(0.4, 1, 0.75, 0.9);
  transition:box-shadow 100ms cubic-bezier(0.4, 1, 0.75, 0.9);
  transition:box-shadow 100ms cubic-bezier(0.4, 1, 0.75, 0.9), -webkit-box-shadow 100ms cubic-bezier(0.4, 1, 0.75, 0.9);
  vertical-align:middle;
  overflow:hidden;
  text-overflow:ellipsis;
  white-space:nowrap;
  word-wrap:normal;
  color:rgba(92, 112, 128, 0.6);
  left:0;
  padding-right:80px;
  position:absolute;
  right:0;
  top:0;
  -webkit-user-select:none;
     -moz-user-select:none;
      -ms-user-select:none;
          user-select:none; }
  .bp3-file-upload-input::-webkit-input-placeholder{
    color:rgba(92, 112, 128, 0.6);
    opacity:1; }
  .bp3-file-upload-input::-moz-placeholder{
    color:rgba(92, 112, 128, 0.6);
    opacity:1; }
  .bp3-file-upload-input:-ms-input-placeholder{
    color:rgba(92, 112, 128, 0.6);
    opacity:1; }
  .bp3-file-upload-input::-ms-input-placeholder{
    color:rgba(92, 112, 128, 0.6);
    opacity:1; }
  .bp3-file-upload-input::placeholder{
    color:rgba(92, 112, 128, 0.6);
    opacity:1; }
  .bp3-file-upload-input:focus, .bp3-file-upload-input.bp3-active{
    -webkit-box-shadow:0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
  .bp3-file-upload-input[type="search"], .bp3-file-upload-input.bp3-round{
    border-radius:30px;
    -webkit-box-sizing:border-box;
            box-sizing:border-box;
    padding-left:10px; }
  .bp3-file-upload-input[readonly]{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.15);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.15); }
  .bp3-file-upload-input:disabled, .bp3-file-upload-input.bp3-disabled{
    background:rgba(206, 217, 224, 0.5);
    -webkit-box-shadow:none;
            box-shadow:none;
    color:rgba(92, 112, 128, 0.6);
    cursor:not-allowed;
    resize:none; }
  .bp3-file-upload-input::after{
    background-color:#f5f8fa;
    background-image:-webkit-gradient(linear, left top, left bottom, from(rgba(255, 255, 255, 0.8)), to(rgba(255, 255, 255, 0)));
    background-image:linear-gradient(to bottom, rgba(255, 255, 255, 0.8), rgba(255, 255, 255, 0));
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
    color:#182026;
    min-height:24px;
    min-width:24px;
    overflow:hidden;
    text-overflow:ellipsis;
    white-space:nowrap;
    word-wrap:normal;
    border-radius:3px;
    content:"Browse";
    line-height:24px;
    margin:3px;
    position:absolute;
    right:0;
    text-align:center;
    top:0;
    width:70px; }
    .bp3-file-upload-input::after:hover{
      background-clip:padding-box;
      background-color:#ebf1f5;
      -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
              box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1); }
    .bp3-file-upload-input::after:active, .bp3-file-upload-input::after.bp3-active{
      background-color:#d8e1e8;
      background-image:none;
      -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 1px 2px rgba(16, 22, 26, 0.2);
              box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 1px 2px rgba(16, 22, 26, 0.2); }
    .bp3-file-upload-input::after:disabled, .bp3-file-upload-input::after.bp3-disabled{
      background-color:rgba(206, 217, 224, 0.5);
      background-image:none;
      -webkit-box-shadow:none;
              box-shadow:none;
      color:rgba(92, 112, 128, 0.6);
      cursor:not-allowed;
      outline:none; }
      .bp3-file-upload-input::after:disabled.bp3-active, .bp3-file-upload-input::after:disabled.bp3-active:hover, .bp3-file-upload-input::after.bp3-disabled.bp3-active, .bp3-file-upload-input::after.bp3-disabled.bp3-active:hover{
        background:rgba(206, 217, 224, 0.7); }
  .bp3-file-upload-input:hover::after{
    background-clip:padding-box;
    background-color:#ebf1f5;
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1); }
  .bp3-file-upload-input:active::after{
    background-color:#d8e1e8;
    background-image:none;
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 1px 2px rgba(16, 22, 26, 0.2);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 1px 2px rgba(16, 22, 26, 0.2); }
  .bp3-large .bp3-file-upload-input{
    font-size:16px;
    height:40px;
    line-height:40px;
    padding-right:95px; }
    .bp3-large .bp3-file-upload-input[type="search"], .bp3-large .bp3-file-upload-input.bp3-round{
      padding:0 15px; }
    .bp3-large .bp3-file-upload-input::after{
      min-height:30px;
      min-width:30px;
      line-height:30px;
      margin:5px;
      width:85px; }
  .bp3-dark .bp3-file-upload-input{
    background:rgba(16, 22, 26, 0.3);
    -webkit-box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
    color:#f5f8fa;
    color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-file-upload-input::-webkit-input-placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-file-upload-input::-moz-placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-file-upload-input:-ms-input-placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-file-upload-input::-ms-input-placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-file-upload-input::placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-file-upload-input:focus{
      -webkit-box-shadow:0 0 0 1px #137cbd, 0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 1px #137cbd, 0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
    .bp3-dark .bp3-file-upload-input[readonly]{
      -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4);
              box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4); }
    .bp3-dark .bp3-file-upload-input:disabled, .bp3-dark .bp3-file-upload-input.bp3-disabled{
      background:rgba(57, 75, 89, 0.5);
      -webkit-box-shadow:none;
              box-shadow:none;
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-file-upload-input::after{
      background-color:#394b59;
      background-image:-webkit-gradient(linear, left top, left bottom, from(rgba(255, 255, 255, 0.05)), to(rgba(255, 255, 255, 0)));
      background-image:linear-gradient(to bottom, rgba(255, 255, 255, 0.05), rgba(255, 255, 255, 0));
      -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
      color:#f5f8fa; }
      .bp3-dark .bp3-file-upload-input::after:hover, .bp3-dark .bp3-file-upload-input::after:active, .bp3-dark .bp3-file-upload-input::after.bp3-active{
        color:#f5f8fa; }
      .bp3-dark .bp3-file-upload-input::after:hover{
        background-color:#30404d;
        -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
                box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4); }
      .bp3-dark .bp3-file-upload-input::after:active, .bp3-dark .bp3-file-upload-input::after.bp3-active{
        background-color:#202b33;
        background-image:none;
        -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.6), inset 0 1px 2px rgba(16, 22, 26, 0.2);
                box-shadow:0 0 0 1px rgba(16, 22, 26, 0.6), inset 0 1px 2px rgba(16, 22, 26, 0.2); }
      .bp3-dark .bp3-file-upload-input::after:disabled, .bp3-dark .bp3-file-upload-input::after.bp3-disabled{
        background-color:rgba(57, 75, 89, 0.5);
        background-image:none;
        -webkit-box-shadow:none;
                box-shadow:none;
        color:rgba(167, 182, 194, 0.6); }
        .bp3-dark .bp3-file-upload-input::after:disabled.bp3-active, .bp3-dark .bp3-file-upload-input::after.bp3-disabled.bp3-active{
          background:rgba(57, 75, 89, 0.7); }
      .bp3-dark .bp3-file-upload-input::after .bp3-button-spinner .bp3-spinner-head{
        background:rgba(16, 22, 26, 0.5);
        stroke:#8a9ba8; }
    .bp3-dark .bp3-file-upload-input:hover::after{
      background-color:#30404d;
      -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4); }
    .bp3-dark .bp3-file-upload-input:active::after{
      background-color:#202b33;
      background-image:none;
      -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.6), inset 0 1px 2px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px rgba(16, 22, 26, 0.6), inset 0 1px 2px rgba(16, 22, 26, 0.2); }
.bp3-file-upload-input::after{
  -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
          box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1); }
.bp3-form-group{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-orient:vertical;
  -webkit-box-direction:normal;
      -ms-flex-direction:column;
          flex-direction:column;
  margin:0 0 15px; }
  .bp3-form-group label.bp3-label{
    margin-bottom:5px; }
  .bp3-form-group .bp3-control{
    margin-top:7px; }
  .bp3-form-group .bp3-form-helper-text{
    color:#5c7080;
    font-size:12px;
    margin-top:5px; }
  .bp3-form-group.bp3-intent-primary .bp3-form-helper-text{
    color:#106ba3; }
  .bp3-form-group.bp3-intent-success .bp3-form-helper-text{
    color:#0d8050; }
  .bp3-form-group.bp3-intent-warning .bp3-form-helper-text{
    color:#bf7326; }
  .bp3-form-group.bp3-intent-danger .bp3-form-helper-text{
    color:#c23030; }
  .bp3-form-group.bp3-inline{
    -webkit-box-align:start;
        -ms-flex-align:start;
            align-items:flex-start;
    -webkit-box-orient:horizontal;
    -webkit-box-direction:normal;
        -ms-flex-direction:row;
            flex-direction:row; }
    .bp3-form-group.bp3-inline.bp3-large label.bp3-label{
      line-height:40px;
      margin:0 10px 0 0; }
    .bp3-form-group.bp3-inline label.bp3-label{
      line-height:30px;
      margin:0 10px 0 0; }
  .bp3-form-group.bp3-disabled .bp3-label,
  .bp3-form-group.bp3-disabled .bp3-text-muted,
  .bp3-form-group.bp3-disabled .bp3-form-helper-text{
    color:rgba(92, 112, 128, 0.6) !important; }
  .bp3-dark .bp3-form-group.bp3-intent-primary .bp3-form-helper-text{
    color:#48aff0; }
  .bp3-dark .bp3-form-group.bp3-intent-success .bp3-form-helper-text{
    color:#3dcc91; }
  .bp3-dark .bp3-form-group.bp3-intent-warning .bp3-form-helper-text{
    color:#ffb366; }
  .bp3-dark .bp3-form-group.bp3-intent-danger .bp3-form-helper-text{
    color:#ff7373; }
  .bp3-dark .bp3-form-group .bp3-form-helper-text{
    color:#a7b6c2; }
  .bp3-dark .bp3-form-group.bp3-disabled .bp3-label,
  .bp3-dark .bp3-form-group.bp3-disabled .bp3-text-muted,
  .bp3-dark .bp3-form-group.bp3-disabled .bp3-form-helper-text{
    color:rgba(167, 182, 194, 0.6) !important; }
.bp3-input-group{
  display:block;
  position:relative; }
  .bp3-input-group .bp3-input{
    position:relative;
    width:100%; }
    .bp3-input-group .bp3-input:not(:first-child){
      padding-left:30px; }
    .bp3-input-group .bp3-input:not(:last-child){
      padding-right:30px; }
  .bp3-input-group .bp3-input-action,
  .bp3-input-group > .bp3-input-left-container,
  .bp3-input-group > .bp3-button,
  .bp3-input-group > .bp3-icon{
    position:absolute;
    top:0; }
    .bp3-input-group .bp3-input-action:first-child,
    .bp3-input-group > .bp3-input-left-container:first-child,
    .bp3-input-group > .bp3-button:first-child,
    .bp3-input-group > .bp3-icon:first-child{
      left:0; }
    .bp3-input-group .bp3-input-action:last-child,
    .bp3-input-group > .bp3-input-left-container:last-child,
    .bp3-input-group > .bp3-button:last-child,
    .bp3-input-group > .bp3-icon:last-child{
      right:0; }
  .bp3-input-group .bp3-button{
    min-height:24px;
    min-width:24px;
    margin:3px;
    padding:0 7px; }
    .bp3-input-group .bp3-button:empty{
      padding:0; }
  .bp3-input-group > .bp3-input-left-container,
  .bp3-input-group > .bp3-icon{
    z-index:1; }
  .bp3-input-group > .bp3-input-left-container > .bp3-icon,
  .bp3-input-group > .bp3-icon{
    color:#5c7080; }
    .bp3-input-group > .bp3-input-left-container > .bp3-icon:empty,
    .bp3-input-group > .bp3-icon:empty{
      font-family:"Icons16", sans-serif;
      font-size:16px;
      font-style:normal;
      font-weight:400;
      line-height:1;
      -moz-osx-font-smoothing:grayscale;
      -webkit-font-smoothing:antialiased; }
  .bp3-input-group > .bp3-input-left-container > .bp3-icon,
  .bp3-input-group > .bp3-icon,
  .bp3-input-group .bp3-input-action > .bp3-spinner{
    margin:7px; }
  .bp3-input-group .bp3-tag{
    margin:5px; }
  .bp3-input-group .bp3-input:not(:focus) + .bp3-button.bp3-minimal:not(:hover):not(:focus),
  .bp3-input-group .bp3-input:not(:focus) + .bp3-input-action .bp3-button.bp3-minimal:not(:hover):not(:focus){
    color:#5c7080; }
    .bp3-dark .bp3-input-group .bp3-input:not(:focus) + .bp3-button.bp3-minimal:not(:hover):not(:focus), .bp3-dark
    .bp3-input-group .bp3-input:not(:focus) + .bp3-input-action .bp3-button.bp3-minimal:not(:hover):not(:focus){
      color:#a7b6c2; }
    .bp3-input-group .bp3-input:not(:focus) + .bp3-button.bp3-minimal:not(:hover):not(:focus) .bp3-icon, .bp3-input-group .bp3-input:not(:focus) + .bp3-button.bp3-minimal:not(:hover):not(:focus) .bp3-icon-standard, .bp3-input-group .bp3-input:not(:focus) + .bp3-button.bp3-minimal:not(:hover):not(:focus) .bp3-icon-large,
    .bp3-input-group .bp3-input:not(:focus) + .bp3-input-action .bp3-button.bp3-minimal:not(:hover):not(:focus) .bp3-icon,
    .bp3-input-group .bp3-input:not(:focus) + .bp3-input-action .bp3-button.bp3-minimal:not(:hover):not(:focus) .bp3-icon-standard,
    .bp3-input-group .bp3-input:not(:focus) + .bp3-input-action .bp3-button.bp3-minimal:not(:hover):not(:focus) .bp3-icon-large{
      color:#5c7080; }
  .bp3-input-group .bp3-input:not(:focus) + .bp3-button.bp3-minimal:disabled,
  .bp3-input-group .bp3-input:not(:focus) + .bp3-input-action .bp3-button.bp3-minimal:disabled{
    color:rgba(92, 112, 128, 0.6) !important; }
    .bp3-input-group .bp3-input:not(:focus) + .bp3-button.bp3-minimal:disabled .bp3-icon, .bp3-input-group .bp3-input:not(:focus) + .bp3-button.bp3-minimal:disabled .bp3-icon-standard, .bp3-input-group .bp3-input:not(:focus) + .bp3-button.bp3-minimal:disabled .bp3-icon-large,
    .bp3-input-group .bp3-input:not(:focus) + .bp3-input-action .bp3-button.bp3-minimal:disabled .bp3-icon,
    .bp3-input-group .bp3-input:not(:focus) + .bp3-input-action .bp3-button.bp3-minimal:disabled .bp3-icon-standard,
    .bp3-input-group .bp3-input:not(:focus) + .bp3-input-action .bp3-button.bp3-minimal:disabled .bp3-icon-large{
      color:rgba(92, 112, 128, 0.6) !important; }
  .bp3-input-group.bp3-disabled{
    cursor:not-allowed; }
    .bp3-input-group.bp3-disabled .bp3-icon{
      color:rgba(92, 112, 128, 0.6); }
  .bp3-input-group.bp3-large .bp3-button{
    min-height:30px;
    min-width:30px;
    margin:5px; }
  .bp3-input-group.bp3-large > .bp3-input-left-container > .bp3-icon,
  .bp3-input-group.bp3-large > .bp3-icon,
  .bp3-input-group.bp3-large .bp3-input-action > .bp3-spinner{
    margin:12px; }
  .bp3-input-group.bp3-large .bp3-input{
    font-size:16px;
    height:40px;
    line-height:40px; }
    .bp3-input-group.bp3-large .bp3-input[type="search"], .bp3-input-group.bp3-large .bp3-input.bp3-round{
      padding:0 15px; }
    .bp3-input-group.bp3-large .bp3-input:not(:first-child){
      padding-left:40px; }
    .bp3-input-group.bp3-large .bp3-input:not(:last-child){
      padding-right:40px; }
  .bp3-input-group.bp3-small .bp3-button{
    min-height:20px;
    min-width:20px;
    margin:2px; }
  .bp3-input-group.bp3-small .bp3-tag{
    min-height:20px;
    min-width:20px;
    margin:2px; }
  .bp3-input-group.bp3-small > .bp3-input-left-container > .bp3-icon,
  .bp3-input-group.bp3-small > .bp3-icon,
  .bp3-input-group.bp3-small .bp3-input-action > .bp3-spinner{
    margin:4px; }
  .bp3-input-group.bp3-small .bp3-input{
    font-size:12px;
    height:24px;
    line-height:24px;
    padding-left:8px;
    padding-right:8px; }
    .bp3-input-group.bp3-small .bp3-input[type="search"], .bp3-input-group.bp3-small .bp3-input.bp3-round{
      padding:0 12px; }
    .bp3-input-group.bp3-small .bp3-input:not(:first-child){
      padding-left:24px; }
    .bp3-input-group.bp3-small .bp3-input:not(:last-child){
      padding-right:24px; }
  .bp3-input-group.bp3-fill{
    -webkit-box-flex:1;
        -ms-flex:1 1 auto;
            flex:1 1 auto;
    width:100%; }
  .bp3-input-group.bp3-round .bp3-button,
  .bp3-input-group.bp3-round .bp3-input,
  .bp3-input-group.bp3-round .bp3-tag{
    border-radius:30px; }
  .bp3-dark .bp3-input-group .bp3-icon{
    color:#a7b6c2; }
  .bp3-dark .bp3-input-group.bp3-disabled .bp3-icon{
    color:rgba(167, 182, 194, 0.6); }
  .bp3-input-group.bp3-intent-primary .bp3-input{
    -webkit-box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px #137cbd, inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px #137cbd, inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-input-group.bp3-intent-primary .bp3-input:focus{
      -webkit-box-shadow:0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-input-group.bp3-intent-primary .bp3-input[readonly]{
      -webkit-box-shadow:inset 0 0 0 1px #137cbd;
              box-shadow:inset 0 0 0 1px #137cbd; }
    .bp3-input-group.bp3-intent-primary .bp3-input:disabled, .bp3-input-group.bp3-intent-primary .bp3-input.bp3-disabled{
      -webkit-box-shadow:none;
              box-shadow:none; }
  .bp3-input-group.bp3-intent-primary > .bp3-icon{
    color:#106ba3; }
    .bp3-dark .bp3-input-group.bp3-intent-primary > .bp3-icon{
      color:#48aff0; }
  .bp3-input-group.bp3-intent-success .bp3-input{
    -webkit-box-shadow:0 0 0 0 rgba(15, 153, 96, 0), 0 0 0 0 rgba(15, 153, 96, 0), inset 0 0 0 1px #0f9960, inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 0 rgba(15, 153, 96, 0), 0 0 0 0 rgba(15, 153, 96, 0), inset 0 0 0 1px #0f9960, inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-input-group.bp3-intent-success .bp3-input:focus{
      -webkit-box-shadow:0 0 0 1px #0f9960, 0 0 0 3px rgba(15, 153, 96, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px #0f9960, 0 0 0 3px rgba(15, 153, 96, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-input-group.bp3-intent-success .bp3-input[readonly]{
      -webkit-box-shadow:inset 0 0 0 1px #0f9960;
              box-shadow:inset 0 0 0 1px #0f9960; }
    .bp3-input-group.bp3-intent-success .bp3-input:disabled, .bp3-input-group.bp3-intent-success .bp3-input.bp3-disabled{
      -webkit-box-shadow:none;
              box-shadow:none; }
  .bp3-input-group.bp3-intent-success > .bp3-icon{
    color:#0d8050; }
    .bp3-dark .bp3-input-group.bp3-intent-success > .bp3-icon{
      color:#3dcc91; }
  .bp3-input-group.bp3-intent-warning .bp3-input{
    -webkit-box-shadow:0 0 0 0 rgba(217, 130, 43, 0), 0 0 0 0 rgba(217, 130, 43, 0), inset 0 0 0 1px #d9822b, inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 0 rgba(217, 130, 43, 0), 0 0 0 0 rgba(217, 130, 43, 0), inset 0 0 0 1px #d9822b, inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-input-group.bp3-intent-warning .bp3-input:focus{
      -webkit-box-shadow:0 0 0 1px #d9822b, 0 0 0 3px rgba(217, 130, 43, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px #d9822b, 0 0 0 3px rgba(217, 130, 43, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-input-group.bp3-intent-warning .bp3-input[readonly]{
      -webkit-box-shadow:inset 0 0 0 1px #d9822b;
              box-shadow:inset 0 0 0 1px #d9822b; }
    .bp3-input-group.bp3-intent-warning .bp3-input:disabled, .bp3-input-group.bp3-intent-warning .bp3-input.bp3-disabled{
      -webkit-box-shadow:none;
              box-shadow:none; }
  .bp3-input-group.bp3-intent-warning > .bp3-icon{
    color:#bf7326; }
    .bp3-dark .bp3-input-group.bp3-intent-warning > .bp3-icon{
      color:#ffb366; }
  .bp3-input-group.bp3-intent-danger .bp3-input{
    -webkit-box-shadow:0 0 0 0 rgba(219, 55, 55, 0), 0 0 0 0 rgba(219, 55, 55, 0), inset 0 0 0 1px #db3737, inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 0 rgba(219, 55, 55, 0), 0 0 0 0 rgba(219, 55, 55, 0), inset 0 0 0 1px #db3737, inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-input-group.bp3-intent-danger .bp3-input:focus{
      -webkit-box-shadow:0 0 0 1px #db3737, 0 0 0 3px rgba(219, 55, 55, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px #db3737, 0 0 0 3px rgba(219, 55, 55, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-input-group.bp3-intent-danger .bp3-input[readonly]{
      -webkit-box-shadow:inset 0 0 0 1px #db3737;
              box-shadow:inset 0 0 0 1px #db3737; }
    .bp3-input-group.bp3-intent-danger .bp3-input:disabled, .bp3-input-group.bp3-intent-danger .bp3-input.bp3-disabled{
      -webkit-box-shadow:none;
              box-shadow:none; }
  .bp3-input-group.bp3-intent-danger > .bp3-icon{
    color:#c23030; }
    .bp3-dark .bp3-input-group.bp3-intent-danger > .bp3-icon{
      color:#ff7373; }
.bp3-input{
  -webkit-appearance:none;
     -moz-appearance:none;
          appearance:none;
  background:#ffffff;
  border:none;
  border-radius:3px;
  -webkit-box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2);
          box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2);
  color:#182026;
  font-size:14px;
  font-weight:400;
  height:30px;
  line-height:30px;
  outline:none;
  padding:0 10px;
  -webkit-transition:-webkit-box-shadow 100ms cubic-bezier(0.4, 1, 0.75, 0.9);
  transition:-webkit-box-shadow 100ms cubic-bezier(0.4, 1, 0.75, 0.9);
  transition:box-shadow 100ms cubic-bezier(0.4, 1, 0.75, 0.9);
  transition:box-shadow 100ms cubic-bezier(0.4, 1, 0.75, 0.9), -webkit-box-shadow 100ms cubic-bezier(0.4, 1, 0.75, 0.9);
  vertical-align:middle; }
  .bp3-input::-webkit-input-placeholder{
    color:rgba(92, 112, 128, 0.6);
    opacity:1; }
  .bp3-input::-moz-placeholder{
    color:rgba(92, 112, 128, 0.6);
    opacity:1; }
  .bp3-input:-ms-input-placeholder{
    color:rgba(92, 112, 128, 0.6);
    opacity:1; }
  .bp3-input::-ms-input-placeholder{
    color:rgba(92, 112, 128, 0.6);
    opacity:1; }
  .bp3-input::placeholder{
    color:rgba(92, 112, 128, 0.6);
    opacity:1; }
  .bp3-input:focus, .bp3-input.bp3-active{
    -webkit-box-shadow:0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
  .bp3-input[type="search"], .bp3-input.bp3-round{
    border-radius:30px;
    -webkit-box-sizing:border-box;
            box-sizing:border-box;
    padding-left:10px; }
  .bp3-input[readonly]{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.15);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.15); }
  .bp3-input:disabled, .bp3-input.bp3-disabled{
    background:rgba(206, 217, 224, 0.5);
    -webkit-box-shadow:none;
            box-shadow:none;
    color:rgba(92, 112, 128, 0.6);
    cursor:not-allowed;
    resize:none; }
  .bp3-input.bp3-large{
    font-size:16px;
    height:40px;
    line-height:40px; }
    .bp3-input.bp3-large[type="search"], .bp3-input.bp3-large.bp3-round{
      padding:0 15px; }
  .bp3-input.bp3-small{
    font-size:12px;
    height:24px;
    line-height:24px;
    padding-left:8px;
    padding-right:8px; }
    .bp3-input.bp3-small[type="search"], .bp3-input.bp3-small.bp3-round{
      padding:0 12px; }
  .bp3-input.bp3-fill{
    -webkit-box-flex:1;
        -ms-flex:1 1 auto;
            flex:1 1 auto;
    width:100%; }
  .bp3-dark .bp3-input{
    background:rgba(16, 22, 26, 0.3);
    -webkit-box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
    color:#f5f8fa; }
    .bp3-dark .bp3-input::-webkit-input-placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-input::-moz-placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-input:-ms-input-placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-input::-ms-input-placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-input::placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-input:focus{
      -webkit-box-shadow:0 0 0 1px #137cbd, 0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 1px #137cbd, 0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
    .bp3-dark .bp3-input[readonly]{
      -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4);
              box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4); }
    .bp3-dark .bp3-input:disabled, .bp3-dark .bp3-input.bp3-disabled{
      background:rgba(57, 75, 89, 0.5);
      -webkit-box-shadow:none;
              box-shadow:none;
      color:rgba(167, 182, 194, 0.6); }
  .bp3-input.bp3-intent-primary{
    -webkit-box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px #137cbd, inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px #137cbd, inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-input.bp3-intent-primary:focus{
      -webkit-box-shadow:0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-input.bp3-intent-primary[readonly]{
      -webkit-box-shadow:inset 0 0 0 1px #137cbd;
              box-shadow:inset 0 0 0 1px #137cbd; }
    .bp3-input.bp3-intent-primary:disabled, .bp3-input.bp3-intent-primary.bp3-disabled{
      -webkit-box-shadow:none;
              box-shadow:none; }
    .bp3-dark .bp3-input.bp3-intent-primary{
      -webkit-box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px #137cbd, inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px #137cbd, inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
      .bp3-dark .bp3-input.bp3-intent-primary:focus{
        -webkit-box-shadow:0 0 0 1px #137cbd, 0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
                box-shadow:0 0 0 1px #137cbd, 0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
      .bp3-dark .bp3-input.bp3-intent-primary[readonly]{
        -webkit-box-shadow:inset 0 0 0 1px #137cbd;
                box-shadow:inset 0 0 0 1px #137cbd; }
      .bp3-dark .bp3-input.bp3-intent-primary:disabled, .bp3-dark .bp3-input.bp3-intent-primary.bp3-disabled{
        -webkit-box-shadow:none;
                box-shadow:none; }
  .bp3-input.bp3-intent-success{
    -webkit-box-shadow:0 0 0 0 rgba(15, 153, 96, 0), 0 0 0 0 rgba(15, 153, 96, 0), inset 0 0 0 1px #0f9960, inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 0 rgba(15, 153, 96, 0), 0 0 0 0 rgba(15, 153, 96, 0), inset 0 0 0 1px #0f9960, inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-input.bp3-intent-success:focus{
      -webkit-box-shadow:0 0 0 1px #0f9960, 0 0 0 3px rgba(15, 153, 96, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px #0f9960, 0 0 0 3px rgba(15, 153, 96, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-input.bp3-intent-success[readonly]{
      -webkit-box-shadow:inset 0 0 0 1px #0f9960;
              box-shadow:inset 0 0 0 1px #0f9960; }
    .bp3-input.bp3-intent-success:disabled, .bp3-input.bp3-intent-success.bp3-disabled{
      -webkit-box-shadow:none;
              box-shadow:none; }
    .bp3-dark .bp3-input.bp3-intent-success{
      -webkit-box-shadow:0 0 0 0 rgba(15, 153, 96, 0), 0 0 0 0 rgba(15, 153, 96, 0), 0 0 0 0 rgba(15, 153, 96, 0), inset 0 0 0 1px #0f9960, inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 0 rgba(15, 153, 96, 0), 0 0 0 0 rgba(15, 153, 96, 0), 0 0 0 0 rgba(15, 153, 96, 0), inset 0 0 0 1px #0f9960, inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
      .bp3-dark .bp3-input.bp3-intent-success:focus{
        -webkit-box-shadow:0 0 0 1px #0f9960, 0 0 0 1px #0f9960, 0 0 0 3px rgba(15, 153, 96, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
                box-shadow:0 0 0 1px #0f9960, 0 0 0 1px #0f9960, 0 0 0 3px rgba(15, 153, 96, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
      .bp3-dark .bp3-input.bp3-intent-success[readonly]{
        -webkit-box-shadow:inset 0 0 0 1px #0f9960;
                box-shadow:inset 0 0 0 1px #0f9960; }
      .bp3-dark .bp3-input.bp3-intent-success:disabled, .bp3-dark .bp3-input.bp3-intent-success.bp3-disabled{
        -webkit-box-shadow:none;
                box-shadow:none; }
  .bp3-input.bp3-intent-warning{
    -webkit-box-shadow:0 0 0 0 rgba(217, 130, 43, 0), 0 0 0 0 rgba(217, 130, 43, 0), inset 0 0 0 1px #d9822b, inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 0 rgba(217, 130, 43, 0), 0 0 0 0 rgba(217, 130, 43, 0), inset 0 0 0 1px #d9822b, inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-input.bp3-intent-warning:focus{
      -webkit-box-shadow:0 0 0 1px #d9822b, 0 0 0 3px rgba(217, 130, 43, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px #d9822b, 0 0 0 3px rgba(217, 130, 43, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-input.bp3-intent-warning[readonly]{
      -webkit-box-shadow:inset 0 0 0 1px #d9822b;
              box-shadow:inset 0 0 0 1px #d9822b; }
    .bp3-input.bp3-intent-warning:disabled, .bp3-input.bp3-intent-warning.bp3-disabled{
      -webkit-box-shadow:none;
              box-shadow:none; }
    .bp3-dark .bp3-input.bp3-intent-warning{
      -webkit-box-shadow:0 0 0 0 rgba(217, 130, 43, 0), 0 0 0 0 rgba(217, 130, 43, 0), 0 0 0 0 rgba(217, 130, 43, 0), inset 0 0 0 1px #d9822b, inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 0 rgba(217, 130, 43, 0), 0 0 0 0 rgba(217, 130, 43, 0), 0 0 0 0 rgba(217, 130, 43, 0), inset 0 0 0 1px #d9822b, inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
      .bp3-dark .bp3-input.bp3-intent-warning:focus{
        -webkit-box-shadow:0 0 0 1px #d9822b, 0 0 0 1px #d9822b, 0 0 0 3px rgba(217, 130, 43, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
                box-shadow:0 0 0 1px #d9822b, 0 0 0 1px #d9822b, 0 0 0 3px rgba(217, 130, 43, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
      .bp3-dark .bp3-input.bp3-intent-warning[readonly]{
        -webkit-box-shadow:inset 0 0 0 1px #d9822b;
                box-shadow:inset 0 0 0 1px #d9822b; }
      .bp3-dark .bp3-input.bp3-intent-warning:disabled, .bp3-dark .bp3-input.bp3-intent-warning.bp3-disabled{
        -webkit-box-shadow:none;
                box-shadow:none; }
  .bp3-input.bp3-intent-danger{
    -webkit-box-shadow:0 0 0 0 rgba(219, 55, 55, 0), 0 0 0 0 rgba(219, 55, 55, 0), inset 0 0 0 1px #db3737, inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 0 rgba(219, 55, 55, 0), 0 0 0 0 rgba(219, 55, 55, 0), inset 0 0 0 1px #db3737, inset 0 0 0 1px rgba(16, 22, 26, 0.15), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-input.bp3-intent-danger:focus{
      -webkit-box-shadow:0 0 0 1px #db3737, 0 0 0 3px rgba(219, 55, 55, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px #db3737, 0 0 0 3px rgba(219, 55, 55, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-input.bp3-intent-danger[readonly]{
      -webkit-box-shadow:inset 0 0 0 1px #db3737;
              box-shadow:inset 0 0 0 1px #db3737; }
    .bp3-input.bp3-intent-danger:disabled, .bp3-input.bp3-intent-danger.bp3-disabled{
      -webkit-box-shadow:none;
              box-shadow:none; }
    .bp3-dark .bp3-input.bp3-intent-danger{
      -webkit-box-shadow:0 0 0 0 rgba(219, 55, 55, 0), 0 0 0 0 rgba(219, 55, 55, 0), 0 0 0 0 rgba(219, 55, 55, 0), inset 0 0 0 1px #db3737, inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 0 rgba(219, 55, 55, 0), 0 0 0 0 rgba(219, 55, 55, 0), 0 0 0 0 rgba(219, 55, 55, 0), inset 0 0 0 1px #db3737, inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
      .bp3-dark .bp3-input.bp3-intent-danger:focus{
        -webkit-box-shadow:0 0 0 1px #db3737, 0 0 0 1px #db3737, 0 0 0 3px rgba(219, 55, 55, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
                box-shadow:0 0 0 1px #db3737, 0 0 0 1px #db3737, 0 0 0 3px rgba(219, 55, 55, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
      .bp3-dark .bp3-input.bp3-intent-danger[readonly]{
        -webkit-box-shadow:inset 0 0 0 1px #db3737;
                box-shadow:inset 0 0 0 1px #db3737; }
      .bp3-dark .bp3-input.bp3-intent-danger:disabled, .bp3-dark .bp3-input.bp3-intent-danger.bp3-disabled{
        -webkit-box-shadow:none;
                box-shadow:none; }
  .bp3-input::-ms-clear{
    display:none; }
textarea.bp3-input{
  max-width:100%;
  padding:10px; }
  textarea.bp3-input, textarea.bp3-input.bp3-large, textarea.bp3-input.bp3-small{
    height:auto;
    line-height:inherit; }
  textarea.bp3-input.bp3-small{
    padding:8px; }
  .bp3-dark textarea.bp3-input{
    background:rgba(16, 22, 26, 0.3);
    -webkit-box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), 0 0 0 0 rgba(19, 124, 189, 0), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
    color:#f5f8fa; }
    .bp3-dark textarea.bp3-input::-webkit-input-placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark textarea.bp3-input::-moz-placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark textarea.bp3-input:-ms-input-placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark textarea.bp3-input::-ms-input-placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark textarea.bp3-input::placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark textarea.bp3-input:focus{
      -webkit-box-shadow:0 0 0 1px #137cbd, 0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 1px #137cbd, 0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
    .bp3-dark textarea.bp3-input[readonly]{
      -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4);
              box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.4); }
    .bp3-dark textarea.bp3-input:disabled, .bp3-dark textarea.bp3-input.bp3-disabled{
      background:rgba(57, 75, 89, 0.5);
      -webkit-box-shadow:none;
              box-shadow:none;
      color:rgba(167, 182, 194, 0.6); }
label.bp3-label{
  display:block;
  margin-bottom:15px;
  margin-top:0; }
  label.bp3-label .bp3-html-select,
  label.bp3-label .bp3-input,
  label.bp3-label .bp3-select,
  label.bp3-label .bp3-slider,
  label.bp3-label .bp3-popover-wrapper{
    display:block;
    margin-top:5px;
    text-transform:none; }
  label.bp3-label .bp3-button-group{
    margin-top:5px; }
  label.bp3-label .bp3-select select,
  label.bp3-label .bp3-html-select select{
    font-weight:400;
    vertical-align:top;
    width:100%; }
  label.bp3-label.bp3-disabled,
  label.bp3-label.bp3-disabled .bp3-text-muted{
    color:rgba(92, 112, 128, 0.6); }
  label.bp3-label.bp3-inline{
    line-height:30px; }
    label.bp3-label.bp3-inline .bp3-html-select,
    label.bp3-label.bp3-inline .bp3-input,
    label.bp3-label.bp3-inline .bp3-input-group,
    label.bp3-label.bp3-inline .bp3-select,
    label.bp3-label.bp3-inline .bp3-popover-wrapper{
      display:inline-block;
      margin:0 0 0 5px;
      vertical-align:top; }
    label.bp3-label.bp3-inline .bp3-button-group{
      margin:0 0 0 5px; }
    label.bp3-label.bp3-inline .bp3-input-group .bp3-input{
      margin-left:0; }
    label.bp3-label.bp3-inline.bp3-large{
      line-height:40px; }
  label.bp3-label:not(.bp3-inline) .bp3-popover-target{
    display:block; }
  .bp3-dark label.bp3-label{
    color:#f5f8fa; }
    .bp3-dark label.bp3-label.bp3-disabled,
    .bp3-dark label.bp3-label.bp3-disabled .bp3-text-muted{
      color:rgba(167, 182, 194, 0.6); }
.bp3-numeric-input .bp3-button-group.bp3-vertical > .bp3-button{
  -webkit-box-flex:1;
      -ms-flex:1 1 14px;
          flex:1 1 14px;
  min-height:0;
  padding:0;
  width:30px; }
  .bp3-numeric-input .bp3-button-group.bp3-vertical > .bp3-button:first-child{
    border-radius:0 3px 0 0; }
  .bp3-numeric-input .bp3-button-group.bp3-vertical > .bp3-button:last-child{
    border-radius:0 0 3px 0; }

.bp3-numeric-input .bp3-button-group.bp3-vertical:first-child > .bp3-button:first-child{
  border-radius:3px 0 0 0; }

.bp3-numeric-input .bp3-button-group.bp3-vertical:first-child > .bp3-button:last-child{
  border-radius:0 0 0 3px; }

.bp3-numeric-input.bp3-large .bp3-button-group.bp3-vertical > .bp3-button{
  width:40px; }

form{
  display:block; }
.bp3-html-select select,
.bp3-select select{
  display:-webkit-inline-box;
  display:-ms-inline-flexbox;
  display:inline-flex;
  -webkit-box-orient:horizontal;
  -webkit-box-direction:normal;
      -ms-flex-direction:row;
          flex-direction:row;
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center;
  border:none;
  border-radius:3px;
  cursor:pointer;
  font-size:14px;
  -webkit-box-pack:center;
      -ms-flex-pack:center;
          justify-content:center;
  padding:5px 10px;
  text-align:left;
  vertical-align:middle;
  background-color:#f5f8fa;
  background-image:-webkit-gradient(linear, left top, left bottom, from(rgba(255, 255, 255, 0.8)), to(rgba(255, 255, 255, 0)));
  background-image:linear-gradient(to bottom, rgba(255, 255, 255, 0.8), rgba(255, 255, 255, 0));
  -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
          box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
  color:#182026;
  -moz-appearance:none;
  -webkit-appearance:none;
  border-radius:3px;
  height:30px;
  padding:0 25px 0 10px;
  width:100%; }
  .bp3-html-select select > *, .bp3-select select > *{
    -webkit-box-flex:0;
        -ms-flex-positive:0;
            flex-grow:0;
    -ms-flex-negative:0;
        flex-shrink:0; }
  .bp3-html-select select > .bp3-fill, .bp3-select select > .bp3-fill{
    -webkit-box-flex:1;
        -ms-flex-positive:1;
            flex-grow:1;
    -ms-flex-negative:1;
        flex-shrink:1; }
  .bp3-html-select select::before,
  .bp3-select select::before, .bp3-html-select select > *, .bp3-select select > *{
    margin-right:7px; }
  .bp3-html-select select:empty::before,
  .bp3-select select:empty::before,
  .bp3-html-select select > :last-child,
  .bp3-select select > :last-child{
    margin-right:0; }
  .bp3-html-select select:hover,
  .bp3-select select:hover{
    background-clip:padding-box;
    background-color:#ebf1f5;
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1); }
  .bp3-html-select select:active,
  .bp3-select select:active, .bp3-html-select select.bp3-active,
  .bp3-select select.bp3-active{
    background-color:#d8e1e8;
    background-image:none;
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 1px 2px rgba(16, 22, 26, 0.2);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 1px 2px rgba(16, 22, 26, 0.2); }
  .bp3-html-select select:disabled,
  .bp3-select select:disabled, .bp3-html-select select.bp3-disabled,
  .bp3-select select.bp3-disabled{
    background-color:rgba(206, 217, 224, 0.5);
    background-image:none;
    -webkit-box-shadow:none;
            box-shadow:none;
    color:rgba(92, 112, 128, 0.6);
    cursor:not-allowed;
    outline:none; }
    .bp3-html-select select:disabled.bp3-active,
    .bp3-select select:disabled.bp3-active, .bp3-html-select select:disabled.bp3-active:hover,
    .bp3-select select:disabled.bp3-active:hover, .bp3-html-select select.bp3-disabled.bp3-active,
    .bp3-select select.bp3-disabled.bp3-active, .bp3-html-select select.bp3-disabled.bp3-active:hover,
    .bp3-select select.bp3-disabled.bp3-active:hover{
      background:rgba(206, 217, 224, 0.7); }

.bp3-html-select.bp3-minimal select,
.bp3-select.bp3-minimal select{
  background:none;
  -webkit-box-shadow:none;
          box-shadow:none; }
  .bp3-html-select.bp3-minimal select:hover,
  .bp3-select.bp3-minimal select:hover{
    background:rgba(167, 182, 194, 0.3);
    -webkit-box-shadow:none;
            box-shadow:none;
    color:#182026;
    text-decoration:none; }
  .bp3-html-select.bp3-minimal select:active,
  .bp3-select.bp3-minimal select:active, .bp3-html-select.bp3-minimal select.bp3-active,
  .bp3-select.bp3-minimal select.bp3-active{
    background:rgba(115, 134, 148, 0.3);
    -webkit-box-shadow:none;
            box-shadow:none;
    color:#182026; }
  .bp3-html-select.bp3-minimal select:disabled,
  .bp3-select.bp3-minimal select:disabled, .bp3-html-select.bp3-minimal select:disabled:hover,
  .bp3-select.bp3-minimal select:disabled:hover, .bp3-html-select.bp3-minimal select.bp3-disabled,
  .bp3-select.bp3-minimal select.bp3-disabled, .bp3-html-select.bp3-minimal select.bp3-disabled:hover,
  .bp3-select.bp3-minimal select.bp3-disabled:hover{
    background:none;
    color:rgba(92, 112, 128, 0.6);
    cursor:not-allowed; }
    .bp3-html-select.bp3-minimal select:disabled.bp3-active,
    .bp3-select.bp3-minimal select:disabled.bp3-active, .bp3-html-select.bp3-minimal select:disabled:hover.bp3-active,
    .bp3-select.bp3-minimal select:disabled:hover.bp3-active, .bp3-html-select.bp3-minimal select.bp3-disabled.bp3-active,
    .bp3-select.bp3-minimal select.bp3-disabled.bp3-active, .bp3-html-select.bp3-minimal select.bp3-disabled:hover.bp3-active,
    .bp3-select.bp3-minimal select.bp3-disabled:hover.bp3-active{
      background:rgba(115, 134, 148, 0.3); }
  .bp3-dark .bp3-html-select.bp3-minimal select, .bp3-html-select.bp3-minimal .bp3-dark select,
  .bp3-dark .bp3-select.bp3-minimal select, .bp3-select.bp3-minimal .bp3-dark select{
    background:none;
    -webkit-box-shadow:none;
            box-shadow:none;
    color:inherit; }
    .bp3-dark .bp3-html-select.bp3-minimal select:hover, .bp3-html-select.bp3-minimal .bp3-dark select:hover,
    .bp3-dark .bp3-select.bp3-minimal select:hover, .bp3-select.bp3-minimal .bp3-dark select:hover, .bp3-dark .bp3-html-select.bp3-minimal select:active, .bp3-html-select.bp3-minimal .bp3-dark select:active,
    .bp3-dark .bp3-select.bp3-minimal select:active, .bp3-select.bp3-minimal .bp3-dark select:active, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-active,
    .bp3-dark .bp3-select.bp3-minimal select.bp3-active, .bp3-select.bp3-minimal .bp3-dark select.bp3-active{
      background:none;
      -webkit-box-shadow:none;
              box-shadow:none; }
    .bp3-dark .bp3-html-select.bp3-minimal select:hover, .bp3-html-select.bp3-minimal .bp3-dark select:hover,
    .bp3-dark .bp3-select.bp3-minimal select:hover, .bp3-select.bp3-minimal .bp3-dark select:hover{
      background:rgba(138, 155, 168, 0.15); }
    .bp3-dark .bp3-html-select.bp3-minimal select:active, .bp3-html-select.bp3-minimal .bp3-dark select:active,
    .bp3-dark .bp3-select.bp3-minimal select:active, .bp3-select.bp3-minimal .bp3-dark select:active, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-active,
    .bp3-dark .bp3-select.bp3-minimal select.bp3-active, .bp3-select.bp3-minimal .bp3-dark select.bp3-active{
      background:rgba(138, 155, 168, 0.3);
      color:#f5f8fa; }
    .bp3-dark .bp3-html-select.bp3-minimal select:disabled, .bp3-html-select.bp3-minimal .bp3-dark select:disabled,
    .bp3-dark .bp3-select.bp3-minimal select:disabled, .bp3-select.bp3-minimal .bp3-dark select:disabled, .bp3-dark .bp3-html-select.bp3-minimal select:disabled:hover, .bp3-html-select.bp3-minimal .bp3-dark select:disabled:hover,
    .bp3-dark .bp3-select.bp3-minimal select:disabled:hover, .bp3-select.bp3-minimal .bp3-dark select:disabled:hover, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-disabled, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-disabled,
    .bp3-dark .bp3-select.bp3-minimal select.bp3-disabled, .bp3-select.bp3-minimal .bp3-dark select.bp3-disabled, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-disabled:hover, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-disabled:hover,
    .bp3-dark .bp3-select.bp3-minimal select.bp3-disabled:hover, .bp3-select.bp3-minimal .bp3-dark select.bp3-disabled:hover{
      background:none;
      color:rgba(167, 182, 194, 0.6);
      cursor:not-allowed; }
      .bp3-dark .bp3-html-select.bp3-minimal select:disabled.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select:disabled.bp3-active,
      .bp3-dark .bp3-select.bp3-minimal select:disabled.bp3-active, .bp3-select.bp3-minimal .bp3-dark select:disabled.bp3-active, .bp3-dark .bp3-html-select.bp3-minimal select:disabled:hover.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select:disabled:hover.bp3-active,
      .bp3-dark .bp3-select.bp3-minimal select:disabled:hover.bp3-active, .bp3-select.bp3-minimal .bp3-dark select:disabled:hover.bp3-active, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-disabled.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-disabled.bp3-active,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-disabled.bp3-active, .bp3-select.bp3-minimal .bp3-dark select.bp3-disabled.bp3-active, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-disabled:hover.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-disabled:hover.bp3-active,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-disabled:hover.bp3-active, .bp3-select.bp3-minimal .bp3-dark select.bp3-disabled:hover.bp3-active{
        background:rgba(138, 155, 168, 0.3); }
  .bp3-html-select.bp3-minimal select.bp3-intent-primary,
  .bp3-select.bp3-minimal select.bp3-intent-primary{
    color:#106ba3; }
    .bp3-html-select.bp3-minimal select.bp3-intent-primary:hover,
    .bp3-select.bp3-minimal select.bp3-intent-primary:hover, .bp3-html-select.bp3-minimal select.bp3-intent-primary:active,
    .bp3-select.bp3-minimal select.bp3-intent-primary:active, .bp3-html-select.bp3-minimal select.bp3-intent-primary.bp3-active,
    .bp3-select.bp3-minimal select.bp3-intent-primary.bp3-active{
      background:none;
      -webkit-box-shadow:none;
              box-shadow:none;
      color:#106ba3; }
    .bp3-html-select.bp3-minimal select.bp3-intent-primary:hover,
    .bp3-select.bp3-minimal select.bp3-intent-primary:hover{
      background:rgba(19, 124, 189, 0.15);
      color:#106ba3; }
    .bp3-html-select.bp3-minimal select.bp3-intent-primary:active,
    .bp3-select.bp3-minimal select.bp3-intent-primary:active, .bp3-html-select.bp3-minimal select.bp3-intent-primary.bp3-active,
    .bp3-select.bp3-minimal select.bp3-intent-primary.bp3-active{
      background:rgba(19, 124, 189, 0.3);
      color:#106ba3; }
    .bp3-html-select.bp3-minimal select.bp3-intent-primary:disabled,
    .bp3-select.bp3-minimal select.bp3-intent-primary:disabled, .bp3-html-select.bp3-minimal select.bp3-intent-primary.bp3-disabled,
    .bp3-select.bp3-minimal select.bp3-intent-primary.bp3-disabled{
      background:none;
      color:rgba(16, 107, 163, 0.5); }
      .bp3-html-select.bp3-minimal select.bp3-intent-primary:disabled.bp3-active,
      .bp3-select.bp3-minimal select.bp3-intent-primary:disabled.bp3-active, .bp3-html-select.bp3-minimal select.bp3-intent-primary.bp3-disabled.bp3-active,
      .bp3-select.bp3-minimal select.bp3-intent-primary.bp3-disabled.bp3-active{
        background:rgba(19, 124, 189, 0.3); }
    .bp3-html-select.bp3-minimal select.bp3-intent-primary .bp3-button-spinner .bp3-spinner-head, .bp3-select.bp3-minimal select.bp3-intent-primary .bp3-button-spinner .bp3-spinner-head{
      stroke:#106ba3; }
    .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-primary, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-primary,
    .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-primary, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-primary{
      color:#48aff0; }
      .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-primary:hover, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-primary:hover,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-primary:hover, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-primary:hover{
        background:rgba(19, 124, 189, 0.2);
        color:#48aff0; }
      .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-primary:active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-primary:active,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-primary:active, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-primary:active, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-primary.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-primary.bp3-active,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-primary.bp3-active, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-primary.bp3-active{
        background:rgba(19, 124, 189, 0.3);
        color:#48aff0; }
      .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-primary:disabled, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-primary:disabled,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-primary:disabled, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-primary:disabled, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-primary.bp3-disabled, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-primary.bp3-disabled,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-primary.bp3-disabled, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-primary.bp3-disabled{
        background:none;
        color:rgba(72, 175, 240, 0.5); }
        .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-primary:disabled.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-primary:disabled.bp3-active,
        .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-primary:disabled.bp3-active, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-primary:disabled.bp3-active, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-primary.bp3-disabled.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-primary.bp3-disabled.bp3-active,
        .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-primary.bp3-disabled.bp3-active, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-primary.bp3-disabled.bp3-active{
          background:rgba(19, 124, 189, 0.3); }
  .bp3-html-select.bp3-minimal select.bp3-intent-success,
  .bp3-select.bp3-minimal select.bp3-intent-success{
    color:#0d8050; }
    .bp3-html-select.bp3-minimal select.bp3-intent-success:hover,
    .bp3-select.bp3-minimal select.bp3-intent-success:hover, .bp3-html-select.bp3-minimal select.bp3-intent-success:active,
    .bp3-select.bp3-minimal select.bp3-intent-success:active, .bp3-html-select.bp3-minimal select.bp3-intent-success.bp3-active,
    .bp3-select.bp3-minimal select.bp3-intent-success.bp3-active{
      background:none;
      -webkit-box-shadow:none;
              box-shadow:none;
      color:#0d8050; }
    .bp3-html-select.bp3-minimal select.bp3-intent-success:hover,
    .bp3-select.bp3-minimal select.bp3-intent-success:hover{
      background:rgba(15, 153, 96, 0.15);
      color:#0d8050; }
    .bp3-html-select.bp3-minimal select.bp3-intent-success:active,
    .bp3-select.bp3-minimal select.bp3-intent-success:active, .bp3-html-select.bp3-minimal select.bp3-intent-success.bp3-active,
    .bp3-select.bp3-minimal select.bp3-intent-success.bp3-active{
      background:rgba(15, 153, 96, 0.3);
      color:#0d8050; }
    .bp3-html-select.bp3-minimal select.bp3-intent-success:disabled,
    .bp3-select.bp3-minimal select.bp3-intent-success:disabled, .bp3-html-select.bp3-minimal select.bp3-intent-success.bp3-disabled,
    .bp3-select.bp3-minimal select.bp3-intent-success.bp3-disabled{
      background:none;
      color:rgba(13, 128, 80, 0.5); }
      .bp3-html-select.bp3-minimal select.bp3-intent-success:disabled.bp3-active,
      .bp3-select.bp3-minimal select.bp3-intent-success:disabled.bp3-active, .bp3-html-select.bp3-minimal select.bp3-intent-success.bp3-disabled.bp3-active,
      .bp3-select.bp3-minimal select.bp3-intent-success.bp3-disabled.bp3-active{
        background:rgba(15, 153, 96, 0.3); }
    .bp3-html-select.bp3-minimal select.bp3-intent-success .bp3-button-spinner .bp3-spinner-head, .bp3-select.bp3-minimal select.bp3-intent-success .bp3-button-spinner .bp3-spinner-head{
      stroke:#0d8050; }
    .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-success, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-success,
    .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-success, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-success{
      color:#3dcc91; }
      .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-success:hover, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-success:hover,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-success:hover, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-success:hover{
        background:rgba(15, 153, 96, 0.2);
        color:#3dcc91; }
      .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-success:active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-success:active,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-success:active, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-success:active, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-success.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-success.bp3-active,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-success.bp3-active, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-success.bp3-active{
        background:rgba(15, 153, 96, 0.3);
        color:#3dcc91; }
      .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-success:disabled, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-success:disabled,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-success:disabled, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-success:disabled, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-success.bp3-disabled, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-success.bp3-disabled,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-success.bp3-disabled, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-success.bp3-disabled{
        background:none;
        color:rgba(61, 204, 145, 0.5); }
        .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-success:disabled.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-success:disabled.bp3-active,
        .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-success:disabled.bp3-active, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-success:disabled.bp3-active, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-success.bp3-disabled.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-success.bp3-disabled.bp3-active,
        .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-success.bp3-disabled.bp3-active, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-success.bp3-disabled.bp3-active{
          background:rgba(15, 153, 96, 0.3); }
  .bp3-html-select.bp3-minimal select.bp3-intent-warning,
  .bp3-select.bp3-minimal select.bp3-intent-warning{
    color:#bf7326; }
    .bp3-html-select.bp3-minimal select.bp3-intent-warning:hover,
    .bp3-select.bp3-minimal select.bp3-intent-warning:hover, .bp3-html-select.bp3-minimal select.bp3-intent-warning:active,
    .bp3-select.bp3-minimal select.bp3-intent-warning:active, .bp3-html-select.bp3-minimal select.bp3-intent-warning.bp3-active,
    .bp3-select.bp3-minimal select.bp3-intent-warning.bp3-active{
      background:none;
      -webkit-box-shadow:none;
              box-shadow:none;
      color:#bf7326; }
    .bp3-html-select.bp3-minimal select.bp3-intent-warning:hover,
    .bp3-select.bp3-minimal select.bp3-intent-warning:hover{
      background:rgba(217, 130, 43, 0.15);
      color:#bf7326; }
    .bp3-html-select.bp3-minimal select.bp3-intent-warning:active,
    .bp3-select.bp3-minimal select.bp3-intent-warning:active, .bp3-html-select.bp3-minimal select.bp3-intent-warning.bp3-active,
    .bp3-select.bp3-minimal select.bp3-intent-warning.bp3-active{
      background:rgba(217, 130, 43, 0.3);
      color:#bf7326; }
    .bp3-html-select.bp3-minimal select.bp3-intent-warning:disabled,
    .bp3-select.bp3-minimal select.bp3-intent-warning:disabled, .bp3-html-select.bp3-minimal select.bp3-intent-warning.bp3-disabled,
    .bp3-select.bp3-minimal select.bp3-intent-warning.bp3-disabled{
      background:none;
      color:rgba(191, 115, 38, 0.5); }
      .bp3-html-select.bp3-minimal select.bp3-intent-warning:disabled.bp3-active,
      .bp3-select.bp3-minimal select.bp3-intent-warning:disabled.bp3-active, .bp3-html-select.bp3-minimal select.bp3-intent-warning.bp3-disabled.bp3-active,
      .bp3-select.bp3-minimal select.bp3-intent-warning.bp3-disabled.bp3-active{
        background:rgba(217, 130, 43, 0.3); }
    .bp3-html-select.bp3-minimal select.bp3-intent-warning .bp3-button-spinner .bp3-spinner-head, .bp3-select.bp3-minimal select.bp3-intent-warning .bp3-button-spinner .bp3-spinner-head{
      stroke:#bf7326; }
    .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-warning, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-warning,
    .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-warning, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-warning{
      color:#ffb366; }
      .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-warning:hover, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-warning:hover,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-warning:hover, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-warning:hover{
        background:rgba(217, 130, 43, 0.2);
        color:#ffb366; }
      .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-warning:active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-warning:active,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-warning:active, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-warning:active, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-warning.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-warning.bp3-active,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-warning.bp3-active, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-warning.bp3-active{
        background:rgba(217, 130, 43, 0.3);
        color:#ffb366; }
      .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-warning:disabled, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-warning:disabled,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-warning:disabled, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-warning:disabled, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-warning.bp3-disabled, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-warning.bp3-disabled,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-warning.bp3-disabled, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-warning.bp3-disabled{
        background:none;
        color:rgba(255, 179, 102, 0.5); }
        .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-warning:disabled.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-warning:disabled.bp3-active,
        .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-warning:disabled.bp3-active, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-warning:disabled.bp3-active, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-warning.bp3-disabled.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-warning.bp3-disabled.bp3-active,
        .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-warning.bp3-disabled.bp3-active, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-warning.bp3-disabled.bp3-active{
          background:rgba(217, 130, 43, 0.3); }
  .bp3-html-select.bp3-minimal select.bp3-intent-danger,
  .bp3-select.bp3-minimal select.bp3-intent-danger{
    color:#c23030; }
    .bp3-html-select.bp3-minimal select.bp3-intent-danger:hover,
    .bp3-select.bp3-minimal select.bp3-intent-danger:hover, .bp3-html-select.bp3-minimal select.bp3-intent-danger:active,
    .bp3-select.bp3-minimal select.bp3-intent-danger:active, .bp3-html-select.bp3-minimal select.bp3-intent-danger.bp3-active,
    .bp3-select.bp3-minimal select.bp3-intent-danger.bp3-active{
      background:none;
      -webkit-box-shadow:none;
              box-shadow:none;
      color:#c23030; }
    .bp3-html-select.bp3-minimal select.bp3-intent-danger:hover,
    .bp3-select.bp3-minimal select.bp3-intent-danger:hover{
      background:rgba(219, 55, 55, 0.15);
      color:#c23030; }
    .bp3-html-select.bp3-minimal select.bp3-intent-danger:active,
    .bp3-select.bp3-minimal select.bp3-intent-danger:active, .bp3-html-select.bp3-minimal select.bp3-intent-danger.bp3-active,
    .bp3-select.bp3-minimal select.bp3-intent-danger.bp3-active{
      background:rgba(219, 55, 55, 0.3);
      color:#c23030; }
    .bp3-html-select.bp3-minimal select.bp3-intent-danger:disabled,
    .bp3-select.bp3-minimal select.bp3-intent-danger:disabled, .bp3-html-select.bp3-minimal select.bp3-intent-danger.bp3-disabled,
    .bp3-select.bp3-minimal select.bp3-intent-danger.bp3-disabled{
      background:none;
      color:rgba(194, 48, 48, 0.5); }
      .bp3-html-select.bp3-minimal select.bp3-intent-danger:disabled.bp3-active,
      .bp3-select.bp3-minimal select.bp3-intent-danger:disabled.bp3-active, .bp3-html-select.bp3-minimal select.bp3-intent-danger.bp3-disabled.bp3-active,
      .bp3-select.bp3-minimal select.bp3-intent-danger.bp3-disabled.bp3-active{
        background:rgba(219, 55, 55, 0.3); }
    .bp3-html-select.bp3-minimal select.bp3-intent-danger .bp3-button-spinner .bp3-spinner-head, .bp3-select.bp3-minimal select.bp3-intent-danger .bp3-button-spinner .bp3-spinner-head{
      stroke:#c23030; }
    .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-danger, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-danger,
    .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-danger, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-danger{
      color:#ff7373; }
      .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-danger:hover, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-danger:hover,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-danger:hover, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-danger:hover{
        background:rgba(219, 55, 55, 0.2);
        color:#ff7373; }
      .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-danger:active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-danger:active,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-danger:active, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-danger:active, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-danger.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-danger.bp3-active,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-danger.bp3-active, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-danger.bp3-active{
        background:rgba(219, 55, 55, 0.3);
        color:#ff7373; }
      .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-danger:disabled, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-danger:disabled,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-danger:disabled, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-danger:disabled, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-danger.bp3-disabled, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-danger.bp3-disabled,
      .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-danger.bp3-disabled, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-danger.bp3-disabled{
        background:none;
        color:rgba(255, 115, 115, 0.5); }
        .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-danger:disabled.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-danger:disabled.bp3-active,
        .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-danger:disabled.bp3-active, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-danger:disabled.bp3-active, .bp3-dark .bp3-html-select.bp3-minimal select.bp3-intent-danger.bp3-disabled.bp3-active, .bp3-html-select.bp3-minimal .bp3-dark select.bp3-intent-danger.bp3-disabled.bp3-active,
        .bp3-dark .bp3-select.bp3-minimal select.bp3-intent-danger.bp3-disabled.bp3-active, .bp3-select.bp3-minimal .bp3-dark select.bp3-intent-danger.bp3-disabled.bp3-active{
          background:rgba(219, 55, 55, 0.3); }

.bp3-html-select.bp3-large select,
.bp3-select.bp3-large select{
  font-size:16px;
  height:40px;
  padding-right:35px; }

.bp3-dark .bp3-html-select select, .bp3-dark .bp3-select select{
  background-color:#394b59;
  background-image:-webkit-gradient(linear, left top, left bottom, from(rgba(255, 255, 255, 0.05)), to(rgba(255, 255, 255, 0)));
  background-image:linear-gradient(to bottom, rgba(255, 255, 255, 0.05), rgba(255, 255, 255, 0));
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
  color:#f5f8fa; }
  .bp3-dark .bp3-html-select select:hover, .bp3-dark .bp3-select select:hover, .bp3-dark .bp3-html-select select:active, .bp3-dark .bp3-select select:active, .bp3-dark .bp3-html-select select.bp3-active, .bp3-dark .bp3-select select.bp3-active{
    color:#f5f8fa; }
  .bp3-dark .bp3-html-select select:hover, .bp3-dark .bp3-select select:hover{
    background-color:#30404d;
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4); }
  .bp3-dark .bp3-html-select select:active, .bp3-dark .bp3-select select:active, .bp3-dark .bp3-html-select select.bp3-active, .bp3-dark .bp3-select select.bp3-active{
    background-color:#202b33;
    background-image:none;
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.6), inset 0 1px 2px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.6), inset 0 1px 2px rgba(16, 22, 26, 0.2); }
  .bp3-dark .bp3-html-select select:disabled, .bp3-dark .bp3-select select:disabled, .bp3-dark .bp3-html-select select.bp3-disabled, .bp3-dark .bp3-select select.bp3-disabled{
    background-color:rgba(57, 75, 89, 0.5);
    background-image:none;
    -webkit-box-shadow:none;
            box-shadow:none;
    color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-html-select select:disabled.bp3-active, .bp3-dark .bp3-select select:disabled.bp3-active, .bp3-dark .bp3-html-select select.bp3-disabled.bp3-active, .bp3-dark .bp3-select select.bp3-disabled.bp3-active{
      background:rgba(57, 75, 89, 0.7); }
  .bp3-dark .bp3-html-select select .bp3-button-spinner .bp3-spinner-head, .bp3-dark .bp3-select select .bp3-button-spinner .bp3-spinner-head{
    background:rgba(16, 22, 26, 0.5);
    stroke:#8a9ba8; }

.bp3-html-select select:disabled,
.bp3-select select:disabled{
  background-color:rgba(206, 217, 224, 0.5);
  -webkit-box-shadow:none;
          box-shadow:none;
  color:rgba(92, 112, 128, 0.6);
  cursor:not-allowed; }

.bp3-html-select .bp3-icon,
.bp3-select .bp3-icon, .bp3-select::after{
  color:#5c7080;
  pointer-events:none;
  position:absolute;
  right:7px;
  top:7px; }
  .bp3-html-select .bp3-disabled.bp3-icon,
  .bp3-select .bp3-disabled.bp3-icon, .bp3-disabled.bp3-select::after{
    color:rgba(92, 112, 128, 0.6); }
.bp3-html-select,
.bp3-select{
  display:inline-block;
  letter-spacing:normal;
  position:relative;
  vertical-align:middle; }
  .bp3-html-select select::-ms-expand,
  .bp3-select select::-ms-expand{
    display:none; }
  .bp3-html-select .bp3-icon,
  .bp3-select .bp3-icon{
    color:#5c7080; }
    .bp3-html-select .bp3-icon:hover,
    .bp3-select .bp3-icon:hover{
      color:#182026; }
    .bp3-dark .bp3-html-select .bp3-icon, .bp3-dark
    .bp3-select .bp3-icon{
      color:#a7b6c2; }
      .bp3-dark .bp3-html-select .bp3-icon:hover, .bp3-dark
      .bp3-select .bp3-icon:hover{
        color:#f5f8fa; }
  .bp3-html-select.bp3-large::after,
  .bp3-html-select.bp3-large .bp3-icon,
  .bp3-select.bp3-large::after,
  .bp3-select.bp3-large .bp3-icon{
    right:12px;
    top:12px; }
  .bp3-html-select.bp3-fill,
  .bp3-html-select.bp3-fill select,
  .bp3-select.bp3-fill,
  .bp3-select.bp3-fill select{
    width:100%; }
  .bp3-dark .bp3-html-select option, .bp3-dark
  .bp3-select option{
    background-color:#30404d;
    color:#f5f8fa; }
  .bp3-dark .bp3-html-select option:disabled, .bp3-dark
  .bp3-select option:disabled{
    color:rgba(167, 182, 194, 0.6); }
  .bp3-dark .bp3-html-select::after, .bp3-dark
  .bp3-select::after{
    color:#a7b6c2; }

.bp3-select::after{
  font-family:"Icons16", sans-serif;
  font-size:16px;
  font-style:normal;
  font-weight:400;
  line-height:1;
  -moz-osx-font-smoothing:grayscale;
  -webkit-font-smoothing:antialiased;
  content:""; }
.bp3-running-text table, table.bp3-html-table{
  border-spacing:0;
  font-size:14px; }
  .bp3-running-text table th, table.bp3-html-table th,
  .bp3-running-text table td,
  table.bp3-html-table td{
    padding:11px;
    text-align:left;
    vertical-align:top; }
  .bp3-running-text table th, table.bp3-html-table th{
    color:#182026;
    font-weight:600; }
  
  .bp3-running-text table td,
  table.bp3-html-table td{
    color:#182026; }
  .bp3-running-text table tbody tr:first-child th, table.bp3-html-table tbody tr:first-child th,
  .bp3-running-text table tbody tr:first-child td,
  table.bp3-html-table tbody tr:first-child td,
  .bp3-running-text table tfoot tr:first-child th,
  table.bp3-html-table tfoot tr:first-child th,
  .bp3-running-text table tfoot tr:first-child td,
  table.bp3-html-table tfoot tr:first-child td{
    -webkit-box-shadow:inset 0 1px 0 0 rgba(16, 22, 26, 0.15);
            box-shadow:inset 0 1px 0 0 rgba(16, 22, 26, 0.15); }
  .bp3-dark .bp3-running-text table th, .bp3-running-text .bp3-dark table th, .bp3-dark table.bp3-html-table th{
    color:#f5f8fa; }
  .bp3-dark .bp3-running-text table td, .bp3-running-text .bp3-dark table td, .bp3-dark table.bp3-html-table td{
    color:#f5f8fa; }
  .bp3-dark .bp3-running-text table tbody tr:first-child th, .bp3-running-text .bp3-dark table tbody tr:first-child th, .bp3-dark table.bp3-html-table tbody tr:first-child th,
  .bp3-dark .bp3-running-text table tbody tr:first-child td,
  .bp3-running-text .bp3-dark table tbody tr:first-child td,
  .bp3-dark table.bp3-html-table tbody tr:first-child td,
  .bp3-dark .bp3-running-text table tfoot tr:first-child th,
  .bp3-running-text .bp3-dark table tfoot tr:first-child th,
  .bp3-dark table.bp3-html-table tfoot tr:first-child th,
  .bp3-dark .bp3-running-text table tfoot tr:first-child td,
  .bp3-running-text .bp3-dark table tfoot tr:first-child td,
  .bp3-dark table.bp3-html-table tfoot tr:first-child td{
    -webkit-box-shadow:inset 0 1px 0 0 rgba(255, 255, 255, 0.15);
            box-shadow:inset 0 1px 0 0 rgba(255, 255, 255, 0.15); }

table.bp3-html-table.bp3-html-table-condensed th,
table.bp3-html-table.bp3-html-table-condensed td, table.bp3-html-table.bp3-small th,
table.bp3-html-table.bp3-small td{
  padding-bottom:6px;
  padding-top:6px; }

table.bp3-html-table.bp3-html-table-striped tbody tr:nth-child(odd) td{
  background:rgba(191, 204, 214, 0.15); }

table.bp3-html-table.bp3-html-table-bordered th:not(:first-child){
  -webkit-box-shadow:inset 1px 0 0 0 rgba(16, 22, 26, 0.15);
          box-shadow:inset 1px 0 0 0 rgba(16, 22, 26, 0.15); }

table.bp3-html-table.bp3-html-table-bordered tbody tr td,
table.bp3-html-table.bp3-html-table-bordered tfoot tr td{
  -webkit-box-shadow:inset 0 1px 0 0 rgba(16, 22, 26, 0.15);
          box-shadow:inset 0 1px 0 0 rgba(16, 22, 26, 0.15); }
  table.bp3-html-table.bp3-html-table-bordered tbody tr td:not(:first-child),
  table.bp3-html-table.bp3-html-table-bordered tfoot tr td:not(:first-child){
    -webkit-box-shadow:inset 1px 1px 0 0 rgba(16, 22, 26, 0.15);
            box-shadow:inset 1px 1px 0 0 rgba(16, 22, 26, 0.15); }

table.bp3-html-table.bp3-html-table-bordered.bp3-html-table-striped tbody tr:not(:first-child) td{
  -webkit-box-shadow:none;
          box-shadow:none; }
  table.bp3-html-table.bp3-html-table-bordered.bp3-html-table-striped tbody tr:not(:first-child) td:not(:first-child){
    -webkit-box-shadow:inset 1px 0 0 0 rgba(16, 22, 26, 0.15);
            box-shadow:inset 1px 0 0 0 rgba(16, 22, 26, 0.15); }

table.bp3-html-table.bp3-interactive tbody tr:hover td{
  background-color:rgba(191, 204, 214, 0.3);
  cursor:pointer; }

table.bp3-html-table.bp3-interactive tbody tr:active td{
  background-color:rgba(191, 204, 214, 0.4); }

.bp3-dark table.bp3-html-table{ }
  .bp3-dark table.bp3-html-table.bp3-html-table-striped tbody tr:nth-child(odd) td{
    background:rgba(92, 112, 128, 0.15); }
  .bp3-dark table.bp3-html-table.bp3-html-table-bordered th:not(:first-child){
    -webkit-box-shadow:inset 1px 0 0 0 rgba(255, 255, 255, 0.15);
            box-shadow:inset 1px 0 0 0 rgba(255, 255, 255, 0.15); }
  .bp3-dark table.bp3-html-table.bp3-html-table-bordered tbody tr td,
  .bp3-dark table.bp3-html-table.bp3-html-table-bordered tfoot tr td{
    -webkit-box-shadow:inset 0 1px 0 0 rgba(255, 255, 255, 0.15);
            box-shadow:inset 0 1px 0 0 rgba(255, 255, 255, 0.15); }
    .bp3-dark table.bp3-html-table.bp3-html-table-bordered tbody tr td:not(:first-child),
    .bp3-dark table.bp3-html-table.bp3-html-table-bordered tfoot tr td:not(:first-child){
      -webkit-box-shadow:inset 1px 1px 0 0 rgba(255, 255, 255, 0.15);
              box-shadow:inset 1px 1px 0 0 rgba(255, 255, 255, 0.15); }
  .bp3-dark table.bp3-html-table.bp3-html-table-bordered.bp3-html-table-striped tbody tr:not(:first-child) td{
    -webkit-box-shadow:inset 1px 0 0 0 rgba(255, 255, 255, 0.15);
            box-shadow:inset 1px 0 0 0 rgba(255, 255, 255, 0.15); }
    .bp3-dark table.bp3-html-table.bp3-html-table-bordered.bp3-html-table-striped tbody tr:not(:first-child) td:first-child{
      -webkit-box-shadow:none;
              box-shadow:none; }
  .bp3-dark table.bp3-html-table.bp3-interactive tbody tr:hover td{
    background-color:rgba(92, 112, 128, 0.3);
    cursor:pointer; }
  .bp3-dark table.bp3-html-table.bp3-interactive tbody tr:active td{
    background-color:rgba(92, 112, 128, 0.4); }

.bp3-key-combo{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-orient:horizontal;
  -webkit-box-direction:normal;
      -ms-flex-direction:row;
          flex-direction:row;
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center; }
  .bp3-key-combo > *{
    -webkit-box-flex:0;
        -ms-flex-positive:0;
            flex-grow:0;
    -ms-flex-negative:0;
        flex-shrink:0; }
  .bp3-key-combo > .bp3-fill{
    -webkit-box-flex:1;
        -ms-flex-positive:1;
            flex-grow:1;
    -ms-flex-negative:1;
        flex-shrink:1; }
  .bp3-key-combo::before,
  .bp3-key-combo > *{
    margin-right:5px; }
  .bp3-key-combo:empty::before,
  .bp3-key-combo > :last-child{
    margin-right:0; }

.bp3-hotkey-dialog{
  padding-bottom:0;
  top:40px; }
  .bp3-hotkey-dialog .bp3-dialog-body{
    margin:0;
    padding:0; }
  .bp3-hotkey-dialog .bp3-hotkey-label{
    -webkit-box-flex:1;
        -ms-flex-positive:1;
            flex-grow:1; }

.bp3-hotkey-column{
  margin:auto;
  max-height:80vh;
  overflow-y:auto;
  padding:30px; }
  .bp3-hotkey-column .bp3-heading{
    margin-bottom:20px; }
    .bp3-hotkey-column .bp3-heading:not(:first-child){
      margin-top:40px; }

.bp3-hotkey{
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center;
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-pack:justify;
      -ms-flex-pack:justify;
          justify-content:space-between;
  margin-left:0;
  margin-right:0; }
  .bp3-hotkey:not(:last-child){
    margin-bottom:10px; }
.bp3-icon{
  display:inline-block;
  -webkit-box-flex:0;
      -ms-flex:0 0 auto;
          flex:0 0 auto;
  vertical-align:text-bottom; }
  .bp3-icon:not(:empty)::before{
    content:"" !important;
    content:unset !important; }
  .bp3-icon > svg{
    display:block; }
    .bp3-icon > svg:not([fill]){
      fill:currentColor; }

.bp3-icon.bp3-intent-primary, .bp3-icon-standard.bp3-intent-primary, .bp3-icon-large.bp3-intent-primary{
  color:#106ba3; }
  .bp3-dark .bp3-icon.bp3-intent-primary, .bp3-dark .bp3-icon-standard.bp3-intent-primary, .bp3-dark .bp3-icon-large.bp3-intent-primary{
    color:#48aff0; }

.bp3-icon.bp3-intent-success, .bp3-icon-standard.bp3-intent-success, .bp3-icon-large.bp3-intent-success{
  color:#0d8050; }
  .bp3-dark .bp3-icon.bp3-intent-success, .bp3-dark .bp3-icon-standard.bp3-intent-success, .bp3-dark .bp3-icon-large.bp3-intent-success{
    color:#3dcc91; }

.bp3-icon.bp3-intent-warning, .bp3-icon-standard.bp3-intent-warning, .bp3-icon-large.bp3-intent-warning{
  color:#bf7326; }
  .bp3-dark .bp3-icon.bp3-intent-warning, .bp3-dark .bp3-icon-standard.bp3-intent-warning, .bp3-dark .bp3-icon-large.bp3-intent-warning{
    color:#ffb366; }

.bp3-icon.bp3-intent-danger, .bp3-icon-standard.bp3-intent-danger, .bp3-icon-large.bp3-intent-danger{
  color:#c23030; }
  .bp3-dark .bp3-icon.bp3-intent-danger, .bp3-dark .bp3-icon-standard.bp3-intent-danger, .bp3-dark .bp3-icon-large.bp3-intent-danger{
    color:#ff7373; }

span.bp3-icon-standard{
  font-family:"Icons16", sans-serif;
  font-size:16px;
  font-style:normal;
  font-weight:400;
  line-height:1;
  -moz-osx-font-smoothing:grayscale;
  -webkit-font-smoothing:antialiased;
  display:inline-block; }

span.bp3-icon-large{
  font-family:"Icons20", sans-serif;
  font-size:20px;
  font-style:normal;
  font-weight:400;
  line-height:1;
  -moz-osx-font-smoothing:grayscale;
  -webkit-font-smoothing:antialiased;
  display:inline-block; }

span.bp3-icon:empty{
  font-family:"Icons20";
  font-size:inherit;
  font-style:normal;
  font-weight:400;
  line-height:1; }
  span.bp3-icon:empty::before{
    -moz-osx-font-smoothing:grayscale;
    -webkit-font-smoothing:antialiased; }

.bp3-icon-add::before{
  content:""; }

.bp3-icon-add-column-left::before{
  content:""; }

.bp3-icon-add-column-right::before{
  content:""; }

.bp3-icon-add-row-bottom::before{
  content:""; }

.bp3-icon-add-row-top::before{
  content:""; }

.bp3-icon-add-to-artifact::before{
  content:""; }

.bp3-icon-add-to-folder::before{
  content:""; }

.bp3-icon-airplane::before{
  content:""; }

.bp3-icon-align-center::before{
  content:""; }

.bp3-icon-align-justify::before{
  content:""; }

.bp3-icon-align-left::before{
  content:""; }

.bp3-icon-align-right::before{
  content:""; }

.bp3-icon-alignment-bottom::before{
  content:""; }

.bp3-icon-alignment-horizontal-center::before{
  content:""; }

.bp3-icon-alignment-left::before{
  content:""; }

.bp3-icon-alignment-right::before{
  content:""; }

.bp3-icon-alignment-top::before{
  content:""; }

.bp3-icon-alignment-vertical-center::before{
  content:""; }

.bp3-icon-annotation::before{
  content:""; }

.bp3-icon-application::before{
  content:""; }

.bp3-icon-applications::before{
  content:""; }

.bp3-icon-archive::before{
  content:""; }

.bp3-icon-arrow-bottom-left::before{
  content:"↙"; }

.bp3-icon-arrow-bottom-right::before{
  content:"↘"; }

.bp3-icon-arrow-down::before{
  content:"↓"; }

.bp3-icon-arrow-left::before{
  content:"←"; }

.bp3-icon-arrow-right::before{
  content:"→"; }

.bp3-icon-arrow-top-left::before{
  content:"↖"; }

.bp3-icon-arrow-top-right::before{
  content:"↗"; }

.bp3-icon-arrow-up::before{
  content:"↑"; }

.bp3-icon-arrows-horizontal::before{
  content:"↔"; }

.bp3-icon-arrows-vertical::before{
  content:"↕"; }

.bp3-icon-asterisk::before{
  content:"*"; }

.bp3-icon-automatic-updates::before{
  content:""; }

.bp3-icon-badge::before{
  content:""; }

.bp3-icon-ban-circle::before{
  content:""; }

.bp3-icon-bank-account::before{
  content:""; }

.bp3-icon-barcode::before{
  content:""; }

.bp3-icon-blank::before{
  content:""; }

.bp3-icon-blocked-person::before{
  content:""; }

.bp3-icon-bold::before{
  content:""; }

.bp3-icon-book::before{
  content:""; }

.bp3-icon-bookmark::before{
  content:""; }

.bp3-icon-box::before{
  content:""; }

.bp3-icon-briefcase::before{
  content:""; }

.bp3-icon-bring-data::before{
  content:""; }

.bp3-icon-build::before{
  content:""; }

.bp3-icon-calculator::before{
  content:""; }

.bp3-icon-calendar::before{
  content:""; }

.bp3-icon-camera::before{
  content:""; }

.bp3-icon-caret-down::before{
  content:"⌄"; }

.bp3-icon-caret-left::before{
  content:"〈"; }

.bp3-icon-caret-right::before{
  content:"〉"; }

.bp3-icon-caret-up::before{
  content:"⌃"; }

.bp3-icon-cell-tower::before{
  content:""; }

.bp3-icon-changes::before{
  content:""; }

.bp3-icon-chart::before{
  content:""; }

.bp3-icon-chat::before{
  content:""; }

.bp3-icon-chevron-backward::before{
  content:""; }

.bp3-icon-chevron-down::before{
  content:""; }

.bp3-icon-chevron-forward::before{
  content:""; }

.bp3-icon-chevron-left::before{
  content:""; }

.bp3-icon-chevron-right::before{
  content:""; }

.bp3-icon-chevron-up::before{
  content:""; }

.bp3-icon-circle::before{
  content:""; }

.bp3-icon-circle-arrow-down::before{
  content:""; }

.bp3-icon-circle-arrow-left::before{
  content:""; }

.bp3-icon-circle-arrow-right::before{
  content:""; }

.bp3-icon-circle-arrow-up::before{
  content:""; }

.bp3-icon-citation::before{
  content:""; }

.bp3-icon-clean::before{
  content:""; }

.bp3-icon-clipboard::before{
  content:""; }

.bp3-icon-cloud::before{
  content:"☁"; }

.bp3-icon-cloud-download::before{
  content:""; }

.bp3-icon-cloud-upload::before{
  content:""; }

.bp3-icon-code::before{
  content:""; }

.bp3-icon-code-block::before{
  content:""; }

.bp3-icon-cog::before{
  content:""; }

.bp3-icon-collapse-all::before{
  content:""; }

.bp3-icon-column-layout::before{
  content:""; }

.bp3-icon-comment::before{
  content:""; }

.bp3-icon-comparison::before{
  content:""; }

.bp3-icon-compass::before{
  content:""; }

.bp3-icon-compressed::before{
  content:""; }

.bp3-icon-confirm::before{
  content:""; }

.bp3-icon-console::before{
  content:""; }

.bp3-icon-contrast::before{
  content:""; }

.bp3-icon-control::before{
  content:""; }

.bp3-icon-credit-card::before{
  content:""; }

.bp3-icon-cross::before{
  content:"✗"; }

.bp3-icon-crown::before{
  content:""; }

.bp3-icon-cube::before{
  content:""; }

.bp3-icon-cube-add::before{
  content:""; }

.bp3-icon-cube-remove::before{
  content:""; }

.bp3-icon-curved-range-chart::before{
  content:""; }

.bp3-icon-cut::before{
  content:""; }

.bp3-icon-dashboard::before{
  content:""; }

.bp3-icon-data-lineage::before{
  content:""; }

.bp3-icon-database::before{
  content:""; }

.bp3-icon-delete::before{
  content:""; }

.bp3-icon-delta::before{
  content:"Δ"; }

.bp3-icon-derive-column::before{
  content:""; }

.bp3-icon-desktop::before{
  content:""; }

.bp3-icon-diagnosis::before{
  content:""; }

.bp3-icon-diagram-tree::before{
  content:""; }

.bp3-icon-direction-left::before{
  content:""; }

.bp3-icon-direction-right::before{
  content:""; }

.bp3-icon-disable::before{
  content:""; }

.bp3-icon-document::before{
  content:""; }

.bp3-icon-document-open::before{
  content:""; }

.bp3-icon-document-share::before{
  content:""; }

.bp3-icon-dollar::before{
  content:"$"; }

.bp3-icon-dot::before{
  content:"•"; }

.bp3-icon-double-caret-horizontal::before{
  content:""; }

.bp3-icon-double-caret-vertical::before{
  content:""; }

.bp3-icon-double-chevron-down::before{
  content:""; }

.bp3-icon-double-chevron-left::before{
  content:""; }

.bp3-icon-double-chevron-right::before{
  content:""; }

.bp3-icon-double-chevron-up::before{
  content:""; }

.bp3-icon-doughnut-chart::before{
  content:""; }

.bp3-icon-download::before{
  content:""; }

.bp3-icon-drag-handle-horizontal::before{
  content:""; }

.bp3-icon-drag-handle-vertical::before{
  content:""; }

.bp3-icon-draw::before{
  content:""; }

.bp3-icon-drive-time::before{
  content:""; }

.bp3-icon-duplicate::before{
  content:""; }

.bp3-icon-edit::before{
  content:"✎"; }

.bp3-icon-eject::before{
  content:"⏏"; }

.bp3-icon-endorsed::before{
  content:""; }

.bp3-icon-envelope::before{
  content:"✉"; }

.bp3-icon-equals::before{
  content:""; }

.bp3-icon-eraser::before{
  content:""; }

.bp3-icon-error::before{
  content:""; }

.bp3-icon-euro::before{
  content:"€"; }

.bp3-icon-exchange::before{
  content:""; }

.bp3-icon-exclude-row::before{
  content:""; }

.bp3-icon-expand-all::before{
  content:""; }

.bp3-icon-export::before{
  content:""; }

.bp3-icon-eye-off::before{
  content:""; }

.bp3-icon-eye-on::before{
  content:""; }

.bp3-icon-eye-open::before{
  content:""; }

.bp3-icon-fast-backward::before{
  content:""; }

.bp3-icon-fast-forward::before{
  content:""; }

.bp3-icon-feed::before{
  content:""; }

.bp3-icon-feed-subscribed::before{
  content:""; }

.bp3-icon-film::before{
  content:""; }

.bp3-icon-filter::before{
  content:""; }

.bp3-icon-filter-keep::before{
  content:""; }

.bp3-icon-filter-list::before{
  content:""; }

.bp3-icon-filter-open::before{
  content:""; }

.bp3-icon-filter-remove::before{
  content:""; }

.bp3-icon-flag::before{
  content:"⚑"; }

.bp3-icon-flame::before{
  content:""; }

.bp3-icon-flash::before{
  content:""; }

.bp3-icon-floppy-disk::before{
  content:""; }

.bp3-icon-flow-branch::before{
  content:""; }

.bp3-icon-flow-end::before{
  content:""; }

.bp3-icon-flow-linear::before{
  content:""; }

.bp3-icon-flow-review::before{
  content:""; }

.bp3-icon-flow-review-branch::before{
  content:""; }

.bp3-icon-flows::before{
  content:""; }

.bp3-icon-folder-close::before{
  content:""; }

.bp3-icon-folder-new::before{
  content:""; }

.bp3-icon-folder-open::before{
  content:""; }

.bp3-icon-folder-shared::before{
  content:""; }

.bp3-icon-folder-shared-open::before{
  content:""; }

.bp3-icon-follower::before{
  content:""; }

.bp3-icon-following::before{
  content:""; }

.bp3-icon-font::before{
  content:""; }

.bp3-icon-fork::before{
  content:""; }

.bp3-icon-form::before{
  content:""; }

.bp3-icon-full-circle::before{
  content:""; }

.bp3-icon-full-stacked-chart::before{
  content:""; }

.bp3-icon-fullscreen::before{
  content:""; }

.bp3-icon-function::before{
  content:""; }

.bp3-icon-gantt-chart::before{
  content:""; }

.bp3-icon-geolocation::before{
  content:""; }

.bp3-icon-geosearch::before{
  content:""; }

.bp3-icon-git-branch::before{
  content:""; }

.bp3-icon-git-commit::before{
  content:""; }

.bp3-icon-git-merge::before{
  content:""; }

.bp3-icon-git-new-branch::before{
  content:""; }

.bp3-icon-git-pull::before{
  content:""; }

.bp3-icon-git-push::before{
  content:""; }

.bp3-icon-git-repo::before{
  content:""; }

.bp3-icon-glass::before{
  content:""; }

.bp3-icon-globe::before{
  content:""; }

.bp3-icon-globe-network::before{
  content:""; }

.bp3-icon-graph::before{
  content:""; }

.bp3-icon-graph-remove::before{
  content:""; }

.bp3-icon-greater-than::before{
  content:""; }

.bp3-icon-greater-than-or-equal-to::before{
  content:""; }

.bp3-icon-grid::before{
  content:""; }

.bp3-icon-grid-view::before{
  content:""; }

.bp3-icon-group-objects::before{
  content:""; }

.bp3-icon-grouped-bar-chart::before{
  content:""; }

.bp3-icon-hand::before{
  content:""; }

.bp3-icon-hand-down::before{
  content:""; }

.bp3-icon-hand-left::before{
  content:""; }

.bp3-icon-hand-right::before{
  content:""; }

.bp3-icon-hand-up::before{
  content:""; }

.bp3-icon-header::before{
  content:""; }

.bp3-icon-header-one::before{
  content:""; }

.bp3-icon-header-two::before{
  content:""; }

.bp3-icon-headset::before{
  content:""; }

.bp3-icon-heart::before{
  content:"♥"; }

.bp3-icon-heart-broken::before{
  content:""; }

.bp3-icon-heat-grid::before{
  content:""; }

.bp3-icon-heatmap::before{
  content:""; }

.bp3-icon-help::before{
  content:"?"; }

.bp3-icon-helper-management::before{
  content:""; }

.bp3-icon-highlight::before{
  content:""; }

.bp3-icon-history::before{
  content:""; }

.bp3-icon-home::before{
  content:"⌂"; }

.bp3-icon-horizontal-bar-chart::before{
  content:""; }

.bp3-icon-horizontal-bar-chart-asc::before{
  content:""; }

.bp3-icon-horizontal-bar-chart-desc::before{
  content:""; }

.bp3-icon-horizontal-distribution::before{
  content:""; }

.bp3-icon-id-number::before{
  content:""; }

.bp3-icon-image-rotate-left::before{
  content:""; }

.bp3-icon-image-rotate-right::before{
  content:""; }

.bp3-icon-import::before{
  content:""; }

.bp3-icon-inbox::before{
  content:""; }

.bp3-icon-inbox-filtered::before{
  content:""; }

.bp3-icon-inbox-geo::before{
  content:""; }

.bp3-icon-inbox-search::before{
  content:""; }

.bp3-icon-inbox-update::before{
  content:""; }

.bp3-icon-info-sign::before{
  content:"ℹ"; }

.bp3-icon-inheritance::before{
  content:""; }

.bp3-icon-inner-join::before{
  content:""; }

.bp3-icon-insert::before{
  content:""; }

.bp3-icon-intersection::before{
  content:""; }

.bp3-icon-ip-address::before{
  content:""; }

.bp3-icon-issue::before{
  content:""; }

.bp3-icon-issue-closed::before{
  content:""; }

.bp3-icon-issue-new::before{
  content:""; }

.bp3-icon-italic::before{
  content:""; }

.bp3-icon-join-table::before{
  content:""; }

.bp3-icon-key::before{
  content:""; }

.bp3-icon-key-backspace::before{
  content:""; }

.bp3-icon-key-command::before{
  content:""; }

.bp3-icon-key-control::before{
  content:""; }

.bp3-icon-key-delete::before{
  content:""; }

.bp3-icon-key-enter::before{
  content:""; }

.bp3-icon-key-escape::before{
  content:""; }

.bp3-icon-key-option::before{
  content:""; }

.bp3-icon-key-shift::before{
  content:""; }

.bp3-icon-key-tab::before{
  content:""; }

.bp3-icon-known-vehicle::before{
  content:""; }

.bp3-icon-lab-test::before{
  content:""; }

.bp3-icon-label::before{
  content:""; }

.bp3-icon-layer::before{
  content:""; }

.bp3-icon-layers::before{
  content:""; }

.bp3-icon-layout::before{
  content:""; }

.bp3-icon-layout-auto::before{
  content:""; }

.bp3-icon-layout-balloon::before{
  content:""; }

.bp3-icon-layout-circle::before{
  content:""; }

.bp3-icon-layout-grid::before{
  content:""; }

.bp3-icon-layout-group-by::before{
  content:""; }

.bp3-icon-layout-hierarchy::before{
  content:""; }

.bp3-icon-layout-linear::before{
  content:""; }

.bp3-icon-layout-skew-grid::before{
  content:""; }

.bp3-icon-layout-sorted-clusters::before{
  content:""; }

.bp3-icon-learning::before{
  content:""; }

.bp3-icon-left-join::before{
  content:""; }

.bp3-icon-less-than::before{
  content:""; }

.bp3-icon-less-than-or-equal-to::before{
  content:""; }

.bp3-icon-lifesaver::before{
  content:""; }

.bp3-icon-lightbulb::before{
  content:""; }

.bp3-icon-link::before{
  content:""; }

.bp3-icon-list::before{
  content:"☰"; }

.bp3-icon-list-columns::before{
  content:""; }

.bp3-icon-list-detail-view::before{
  content:""; }

.bp3-icon-locate::before{
  content:""; }

.bp3-icon-lock::before{
  content:""; }

.bp3-icon-log-in::before{
  content:""; }

.bp3-icon-log-out::before{
  content:""; }

.bp3-icon-manual::before{
  content:""; }

.bp3-icon-manually-entered-data::before{
  content:""; }

.bp3-icon-map::before{
  content:""; }

.bp3-icon-map-create::before{
  content:""; }

.bp3-icon-map-marker::before{
  content:""; }

.bp3-icon-maximize::before{
  content:""; }

.bp3-icon-media::before{
  content:""; }

.bp3-icon-menu::before{
  content:""; }

.bp3-icon-menu-closed::before{
  content:""; }

.bp3-icon-menu-open::before{
  content:""; }

.bp3-icon-merge-columns::before{
  content:""; }

.bp3-icon-merge-links::before{
  content:""; }

.bp3-icon-minimize::before{
  content:""; }

.bp3-icon-minus::before{
  content:"−"; }

.bp3-icon-mobile-phone::before{
  content:""; }

.bp3-icon-mobile-video::before{
  content:""; }

.bp3-icon-moon::before{
  content:""; }

.bp3-icon-more::before{
  content:""; }

.bp3-icon-mountain::before{
  content:""; }

.bp3-icon-move::before{
  content:""; }

.bp3-icon-mugshot::before{
  content:""; }

.bp3-icon-multi-select::before{
  content:""; }

.bp3-icon-music::before{
  content:""; }

.bp3-icon-new-drawing::before{
  content:""; }

.bp3-icon-new-grid-item::before{
  content:""; }

.bp3-icon-new-layer::before{
  content:""; }

.bp3-icon-new-layers::before{
  content:""; }

.bp3-icon-new-link::before{
  content:""; }

.bp3-icon-new-object::before{
  content:""; }

.bp3-icon-new-person::before{
  content:""; }

.bp3-icon-new-prescription::before{
  content:""; }

.bp3-icon-new-text-box::before{
  content:""; }

.bp3-icon-ninja::before{
  content:""; }

.bp3-icon-not-equal-to::before{
  content:""; }

.bp3-icon-notifications::before{
  content:""; }

.bp3-icon-notifications-updated::before{
  content:""; }

.bp3-icon-numbered-list::before{
  content:""; }

.bp3-icon-numerical::before{
  content:""; }

.bp3-icon-office::before{
  content:""; }

.bp3-icon-offline::before{
  content:""; }

.bp3-icon-oil-field::before{
  content:""; }

.bp3-icon-one-column::before{
  content:""; }

.bp3-icon-outdated::before{
  content:""; }

.bp3-icon-page-layout::before{
  content:""; }

.bp3-icon-panel-stats::before{
  content:""; }

.bp3-icon-panel-table::before{
  content:""; }

.bp3-icon-paperclip::before{
  content:""; }

.bp3-icon-paragraph::before{
  content:""; }

.bp3-icon-path::before{
  content:""; }

.bp3-icon-path-search::before{
  content:""; }

.bp3-icon-pause::before{
  content:""; }

.bp3-icon-people::before{
  content:""; }

.bp3-icon-percentage::before{
  content:""; }

.bp3-icon-person::before{
  content:""; }

.bp3-icon-phone::before{
  content:"☎"; }

.bp3-icon-pie-chart::before{
  content:""; }

.bp3-icon-pin::before{
  content:""; }

.bp3-icon-pivot::before{
  content:""; }

.bp3-icon-pivot-table::before{
  content:""; }

.bp3-icon-play::before{
  content:""; }

.bp3-icon-plus::before{
  content:"+"; }

.bp3-icon-polygon-filter::before{
  content:""; }

.bp3-icon-power::before{
  content:""; }

.bp3-icon-predictive-analysis::before{
  content:""; }

.bp3-icon-prescription::before{
  content:""; }

.bp3-icon-presentation::before{
  content:""; }

.bp3-icon-print::before{
  content:"⎙"; }

.bp3-icon-projects::before{
  content:""; }

.bp3-icon-properties::before{
  content:""; }

.bp3-icon-property::before{
  content:""; }

.bp3-icon-publish-function::before{
  content:""; }

.bp3-icon-pulse::before{
  content:""; }

.bp3-icon-random::before{
  content:""; }

.bp3-icon-record::before{
  content:""; }

.bp3-icon-redo::before{
  content:""; }

.bp3-icon-refresh::before{
  content:""; }

.bp3-icon-regression-chart::before{
  content:""; }

.bp3-icon-remove::before{
  content:""; }

.bp3-icon-remove-column::before{
  content:""; }

.bp3-icon-remove-column-left::before{
  content:""; }

.bp3-icon-remove-column-right::before{
  content:""; }

.bp3-icon-remove-row-bottom::before{
  content:""; }

.bp3-icon-remove-row-top::before{
  content:""; }

.bp3-icon-repeat::before{
  content:""; }

.bp3-icon-reset::before{
  content:""; }

.bp3-icon-resolve::before{
  content:""; }

.bp3-icon-rig::before{
  content:""; }

.bp3-icon-right-join::before{
  content:""; }

.bp3-icon-ring::before{
  content:""; }

.bp3-icon-rotate-document::before{
  content:""; }

.bp3-icon-rotate-page::before{
  content:""; }

.bp3-icon-satellite::before{
  content:""; }

.bp3-icon-saved::before{
  content:""; }

.bp3-icon-scatter-plot::before{
  content:""; }

.bp3-icon-search::before{
  content:""; }

.bp3-icon-search-around::before{
  content:""; }

.bp3-icon-search-template::before{
  content:""; }

.bp3-icon-search-text::before{
  content:""; }

.bp3-icon-segmented-control::before{
  content:""; }

.bp3-icon-select::before{
  content:""; }

.bp3-icon-selection::before{
  content:"⦿"; }

.bp3-icon-send-to::before{
  content:""; }

.bp3-icon-send-to-graph::before{
  content:""; }

.bp3-icon-send-to-map::before{
  content:""; }

.bp3-icon-series-add::before{
  content:""; }

.bp3-icon-series-configuration::before{
  content:""; }

.bp3-icon-series-derived::before{
  content:""; }

.bp3-icon-series-filtered::before{
  content:""; }

.bp3-icon-series-search::before{
  content:""; }

.bp3-icon-settings::before{
  content:""; }

.bp3-icon-share::before{
  content:""; }

.bp3-icon-shield::before{
  content:""; }

.bp3-icon-shop::before{
  content:""; }

.bp3-icon-shopping-cart::before{
  content:""; }

.bp3-icon-signal-search::before{
  content:""; }

.bp3-icon-sim-card::before{
  content:""; }

.bp3-icon-slash::before{
  content:""; }

.bp3-icon-small-cross::before{
  content:""; }

.bp3-icon-small-minus::before{
  content:""; }

.bp3-icon-small-plus::before{
  content:""; }

.bp3-icon-small-tick::before{
  content:""; }

.bp3-icon-snowflake::before{
  content:""; }

.bp3-icon-social-media::before{
  content:""; }

.bp3-icon-sort::before{
  content:""; }

.bp3-icon-sort-alphabetical::before{
  content:""; }

.bp3-icon-sort-alphabetical-desc::before{
  content:""; }

.bp3-icon-sort-asc::before{
  content:""; }

.bp3-icon-sort-desc::before{
  content:""; }

.bp3-icon-sort-numerical::before{
  content:""; }

.bp3-icon-sort-numerical-desc::before{
  content:""; }

.bp3-icon-split-columns::before{
  content:""; }

.bp3-icon-square::before{
  content:""; }

.bp3-icon-stacked-chart::before{
  content:""; }

.bp3-icon-star::before{
  content:"★"; }

.bp3-icon-star-empty::before{
  content:"☆"; }

.bp3-icon-step-backward::before{
  content:""; }

.bp3-icon-step-chart::before{
  content:""; }

.bp3-icon-step-forward::before{
  content:""; }

.bp3-icon-stop::before{
  content:""; }

.bp3-icon-stopwatch::before{
  content:""; }

.bp3-icon-strikethrough::before{
  content:""; }

.bp3-icon-style::before{
  content:""; }

.bp3-icon-swap-horizontal::before{
  content:""; }

.bp3-icon-swap-vertical::before{
  content:""; }

.bp3-icon-symbol-circle::before{
  content:""; }

.bp3-icon-symbol-cross::before{
  content:""; }

.bp3-icon-symbol-diamond::before{
  content:""; }

.bp3-icon-symbol-square::before{
  content:""; }

.bp3-icon-symbol-triangle-down::before{
  content:""; }

.bp3-icon-symbol-triangle-up::before{
  content:""; }

.bp3-icon-tag::before{
  content:""; }

.bp3-icon-take-action::before{
  content:""; }

.bp3-icon-taxi::before{
  content:""; }

.bp3-icon-text-highlight::before{
  content:""; }

.bp3-icon-th::before{
  content:""; }

.bp3-icon-th-derived::before{
  content:""; }

.bp3-icon-th-disconnect::before{
  content:""; }

.bp3-icon-th-filtered::before{
  content:""; }

.bp3-icon-th-list::before{
  content:""; }

.bp3-icon-thumbs-down::before{
  content:""; }

.bp3-icon-thumbs-up::before{
  content:""; }

.bp3-icon-tick::before{
  content:"✓"; }

.bp3-icon-tick-circle::before{
  content:""; }

.bp3-icon-time::before{
  content:"⏲"; }

.bp3-icon-timeline-area-chart::before{
  content:""; }

.bp3-icon-timeline-bar-chart::before{
  content:""; }

.bp3-icon-timeline-events::before{
  content:""; }

.bp3-icon-timeline-line-chart::before{
  content:""; }

.bp3-icon-tint::before{
  content:""; }

.bp3-icon-torch::before{
  content:""; }

.bp3-icon-tractor::before{
  content:""; }

.bp3-icon-train::before{
  content:""; }

.bp3-icon-translate::before{
  content:""; }

.bp3-icon-trash::before{
  content:""; }

.bp3-icon-tree::before{
  content:""; }

.bp3-icon-trending-down::before{
  content:""; }

.bp3-icon-trending-up::before{
  content:""; }

.bp3-icon-truck::before{
  content:""; }

.bp3-icon-two-columns::before{
  content:""; }

.bp3-icon-unarchive::before{
  content:""; }

.bp3-icon-underline::before{
  content:"⎁"; }

.bp3-icon-undo::before{
  content:"⎌"; }

.bp3-icon-ungroup-objects::before{
  content:""; }

.bp3-icon-unknown-vehicle::before{
  content:""; }

.bp3-icon-unlock::before{
  content:""; }

.bp3-icon-unpin::before{
  content:""; }

.bp3-icon-unresolve::before{
  content:""; }

.bp3-icon-updated::before{
  content:""; }

.bp3-icon-upload::before{
  content:""; }

.bp3-icon-user::before{
  content:""; }

.bp3-icon-variable::before{
  content:""; }

.bp3-icon-vertical-bar-chart-asc::before{
  content:""; }

.bp3-icon-vertical-bar-chart-desc::before{
  content:""; }

.bp3-icon-vertical-distribution::before{
  content:""; }

.bp3-icon-video::before{
  content:""; }

.bp3-icon-volume-down::before{
  content:""; }

.bp3-icon-volume-off::before{
  content:""; }

.bp3-icon-volume-up::before{
  content:""; }

.bp3-icon-walk::before{
  content:""; }

.bp3-icon-warning-sign::before{
  content:""; }

.bp3-icon-waterfall-chart::before{
  content:""; }

.bp3-icon-widget::before{
  content:""; }

.bp3-icon-widget-button::before{
  content:""; }

.bp3-icon-widget-footer::before{
  content:""; }

.bp3-icon-widget-header::before{
  content:""; }

.bp3-icon-wrench::before{
  content:""; }

.bp3-icon-zoom-in::before{
  content:""; }

.bp3-icon-zoom-out::before{
  content:""; }

.bp3-icon-zoom-to-fit::before{
  content:""; }
.bp3-submenu > .bp3-popover-wrapper{
  display:block; }

.bp3-submenu .bp3-popover-target{
  display:block; }
  .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-menu-item{ }

.bp3-submenu.bp3-popover{
  -webkit-box-shadow:none;
          box-shadow:none;
  padding:0 5px; }
  .bp3-submenu.bp3-popover > .bp3-popover-content{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 2px 4px rgba(16, 22, 26, 0.2), 0 8px 24px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 2px 4px rgba(16, 22, 26, 0.2), 0 8px 24px rgba(16, 22, 26, 0.2); }
  .bp3-dark .bp3-submenu.bp3-popover, .bp3-submenu.bp3-popover.bp3-dark{
    -webkit-box-shadow:none;
            box-shadow:none; }
    .bp3-dark .bp3-submenu.bp3-popover > .bp3-popover-content, .bp3-submenu.bp3-popover.bp3-dark > .bp3-popover-content{
      -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 2px 4px rgba(16, 22, 26, 0.4), 0 8px 24px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 2px 4px rgba(16, 22, 26, 0.4), 0 8px 24px rgba(16, 22, 26, 0.4); }
.bp3-menu{
  background:#ffffff;
  border-radius:3px;
  color:#182026;
  list-style:none;
  margin:0;
  min-width:180px;
  padding:5px;
  text-align:left; }

.bp3-menu-divider{
  border-top:1px solid rgba(16, 22, 26, 0.15);
  display:block;
  margin:5px; }
  .bp3-dark .bp3-menu-divider{
    border-top-color:rgba(255, 255, 255, 0.15); }

.bp3-menu-item{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-orient:horizontal;
  -webkit-box-direction:normal;
      -ms-flex-direction:row;
          flex-direction:row;
  -webkit-box-align:start;
      -ms-flex-align:start;
          align-items:flex-start;
  border-radius:2px;
  color:inherit;
  line-height:20px;
  padding:5px 7px;
  text-decoration:none;
  -webkit-user-select:none;
     -moz-user-select:none;
      -ms-user-select:none;
          user-select:none; }
  .bp3-menu-item > *{
    -webkit-box-flex:0;
        -ms-flex-positive:0;
            flex-grow:0;
    -ms-flex-negative:0;
        flex-shrink:0; }
  .bp3-menu-item > .bp3-fill{
    -webkit-box-flex:1;
        -ms-flex-positive:1;
            flex-grow:1;
    -ms-flex-negative:1;
        flex-shrink:1; }
  .bp3-menu-item::before,
  .bp3-menu-item > *{
    margin-right:7px; }
  .bp3-menu-item:empty::before,
  .bp3-menu-item > :last-child{
    margin-right:0; }
  .bp3-menu-item > .bp3-fill{
    word-break:break-word; }
  .bp3-menu-item:hover, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-menu-item{
    background-color:rgba(167, 182, 194, 0.3);
    cursor:pointer;
    text-decoration:none; }
  .bp3-menu-item.bp3-disabled{
    background-color:inherit;
    color:rgba(92, 112, 128, 0.6);
    cursor:not-allowed; }
  .bp3-dark .bp3-menu-item{
    color:inherit; }
    .bp3-dark .bp3-menu-item:hover, .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-menu-item, .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-menu-item{
      background-color:rgba(138, 155, 168, 0.15);
      color:inherit; }
    .bp3-dark .bp3-menu-item.bp3-disabled{
      background-color:inherit;
      color:rgba(167, 182, 194, 0.6); }
  .bp3-menu-item.bp3-intent-primary{
    color:#106ba3; }
    .bp3-menu-item.bp3-intent-primary .bp3-icon{
      color:inherit; }
    .bp3-menu-item.bp3-intent-primary::before, .bp3-menu-item.bp3-intent-primary::after,
    .bp3-menu-item.bp3-intent-primary .bp3-menu-item-label{
      color:#106ba3; }
    .bp3-menu-item.bp3-intent-primary:hover, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-primary.bp3-menu-item, .bp3-menu-item.bp3-intent-primary.bp3-active{
      background-color:#137cbd; }
    .bp3-menu-item.bp3-intent-primary:active{
      background-color:#106ba3; }
    .bp3-menu-item.bp3-intent-primary:hover, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-primary.bp3-menu-item, .bp3-menu-item.bp3-intent-primary:hover::before, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-primary.bp3-menu-item::before, .bp3-menu-item.bp3-intent-primary:hover::after, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-primary.bp3-menu-item::after,
    .bp3-menu-item.bp3-intent-primary:hover .bp3-menu-item-label,
    .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-primary.bp3-menu-item .bp3-menu-item-label, .bp3-menu-item.bp3-intent-primary:active, .bp3-menu-item.bp3-intent-primary:active::before, .bp3-menu-item.bp3-intent-primary:active::after,
    .bp3-menu-item.bp3-intent-primary:active .bp3-menu-item-label, .bp3-menu-item.bp3-intent-primary.bp3-active, .bp3-menu-item.bp3-intent-primary.bp3-active::before, .bp3-menu-item.bp3-intent-primary.bp3-active::after,
    .bp3-menu-item.bp3-intent-primary.bp3-active .bp3-menu-item-label{
      color:#ffffff; }
  .bp3-menu-item.bp3-intent-success{
    color:#0d8050; }
    .bp3-menu-item.bp3-intent-success .bp3-icon{
      color:inherit; }
    .bp3-menu-item.bp3-intent-success::before, .bp3-menu-item.bp3-intent-success::after,
    .bp3-menu-item.bp3-intent-success .bp3-menu-item-label{
      color:#0d8050; }
    .bp3-menu-item.bp3-intent-success:hover, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-success.bp3-menu-item, .bp3-menu-item.bp3-intent-success.bp3-active{
      background-color:#0f9960; }
    .bp3-menu-item.bp3-intent-success:active{
      background-color:#0d8050; }
    .bp3-menu-item.bp3-intent-success:hover, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-success.bp3-menu-item, .bp3-menu-item.bp3-intent-success:hover::before, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-success.bp3-menu-item::before, .bp3-menu-item.bp3-intent-success:hover::after, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-success.bp3-menu-item::after,
    .bp3-menu-item.bp3-intent-success:hover .bp3-menu-item-label,
    .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-success.bp3-menu-item .bp3-menu-item-label, .bp3-menu-item.bp3-intent-success:active, .bp3-menu-item.bp3-intent-success:active::before, .bp3-menu-item.bp3-intent-success:active::after,
    .bp3-menu-item.bp3-intent-success:active .bp3-menu-item-label, .bp3-menu-item.bp3-intent-success.bp3-active, .bp3-menu-item.bp3-intent-success.bp3-active::before, .bp3-menu-item.bp3-intent-success.bp3-active::after,
    .bp3-menu-item.bp3-intent-success.bp3-active .bp3-menu-item-label{
      color:#ffffff; }
  .bp3-menu-item.bp3-intent-warning{
    color:#bf7326; }
    .bp3-menu-item.bp3-intent-warning .bp3-icon{
      color:inherit; }
    .bp3-menu-item.bp3-intent-warning::before, .bp3-menu-item.bp3-intent-warning::after,
    .bp3-menu-item.bp3-intent-warning .bp3-menu-item-label{
      color:#bf7326; }
    .bp3-menu-item.bp3-intent-warning:hover, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-warning.bp3-menu-item, .bp3-menu-item.bp3-intent-warning.bp3-active{
      background-color:#d9822b; }
    .bp3-menu-item.bp3-intent-warning:active{
      background-color:#bf7326; }
    .bp3-menu-item.bp3-intent-warning:hover, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-warning.bp3-menu-item, .bp3-menu-item.bp3-intent-warning:hover::before, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-warning.bp3-menu-item::before, .bp3-menu-item.bp3-intent-warning:hover::after, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-warning.bp3-menu-item::after,
    .bp3-menu-item.bp3-intent-warning:hover .bp3-menu-item-label,
    .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-warning.bp3-menu-item .bp3-menu-item-label, .bp3-menu-item.bp3-intent-warning:active, .bp3-menu-item.bp3-intent-warning:active::before, .bp3-menu-item.bp3-intent-warning:active::after,
    .bp3-menu-item.bp3-intent-warning:active .bp3-menu-item-label, .bp3-menu-item.bp3-intent-warning.bp3-active, .bp3-menu-item.bp3-intent-warning.bp3-active::before, .bp3-menu-item.bp3-intent-warning.bp3-active::after,
    .bp3-menu-item.bp3-intent-warning.bp3-active .bp3-menu-item-label{
      color:#ffffff; }
  .bp3-menu-item.bp3-intent-danger{
    color:#c23030; }
    .bp3-menu-item.bp3-intent-danger .bp3-icon{
      color:inherit; }
    .bp3-menu-item.bp3-intent-danger::before, .bp3-menu-item.bp3-intent-danger::after,
    .bp3-menu-item.bp3-intent-danger .bp3-menu-item-label{
      color:#c23030; }
    .bp3-menu-item.bp3-intent-danger:hover, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-danger.bp3-menu-item, .bp3-menu-item.bp3-intent-danger.bp3-active{
      background-color:#db3737; }
    .bp3-menu-item.bp3-intent-danger:active{
      background-color:#c23030; }
    .bp3-menu-item.bp3-intent-danger:hover, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-danger.bp3-menu-item, .bp3-menu-item.bp3-intent-danger:hover::before, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-danger.bp3-menu-item::before, .bp3-menu-item.bp3-intent-danger:hover::after, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-danger.bp3-menu-item::after,
    .bp3-menu-item.bp3-intent-danger:hover .bp3-menu-item-label,
    .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-danger.bp3-menu-item .bp3-menu-item-label, .bp3-menu-item.bp3-intent-danger:active, .bp3-menu-item.bp3-intent-danger:active::before, .bp3-menu-item.bp3-intent-danger:active::after,
    .bp3-menu-item.bp3-intent-danger:active .bp3-menu-item-label, .bp3-menu-item.bp3-intent-danger.bp3-active, .bp3-menu-item.bp3-intent-danger.bp3-active::before, .bp3-menu-item.bp3-intent-danger.bp3-active::after,
    .bp3-menu-item.bp3-intent-danger.bp3-active .bp3-menu-item-label{
      color:#ffffff; }
  .bp3-menu-item::before{
    font-family:"Icons16", sans-serif;
    font-size:16px;
    font-style:normal;
    font-weight:400;
    line-height:1;
    -moz-osx-font-smoothing:grayscale;
    -webkit-font-smoothing:antialiased;
    margin-right:7px; }
  .bp3-menu-item::before,
  .bp3-menu-item > .bp3-icon{
    color:#5c7080;
    margin-top:2px; }
  .bp3-menu-item .bp3-menu-item-label{
    color:#5c7080; }
  .bp3-menu-item:hover, .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-menu-item{
    color:inherit; }
  .bp3-menu-item.bp3-active, .bp3-menu-item:active{
    background-color:rgba(115, 134, 148, 0.3); }
  .bp3-menu-item.bp3-disabled{
    background-color:inherit !important;
    color:rgba(92, 112, 128, 0.6) !important;
    cursor:not-allowed !important;
    outline:none !important; }
    .bp3-menu-item.bp3-disabled::before,
    .bp3-menu-item.bp3-disabled > .bp3-icon,
    .bp3-menu-item.bp3-disabled .bp3-menu-item-label{
      color:rgba(92, 112, 128, 0.6) !important; }
  .bp3-large .bp3-menu-item{
    font-size:16px;
    line-height:22px;
    padding:9px 7px; }
    .bp3-large .bp3-menu-item .bp3-icon{
      margin-top:3px; }
    .bp3-large .bp3-menu-item::before{
      font-family:"Icons20", sans-serif;
      font-size:20px;
      font-style:normal;
      font-weight:400;
      line-height:1;
      -moz-osx-font-smoothing:grayscale;
      -webkit-font-smoothing:antialiased;
      margin-right:10px;
      margin-top:1px; }

button.bp3-menu-item{
  background:none;
  border:none;
  text-align:left;
  width:100%; }
.bp3-menu-header{
  border-top:1px solid rgba(16, 22, 26, 0.15);
  display:block;
  margin:5px;
  cursor:default;
  padding-left:2px; }
  .bp3-dark .bp3-menu-header{
    border-top-color:rgba(255, 255, 255, 0.15); }
  .bp3-menu-header:first-of-type{
    border-top:none; }
  .bp3-menu-header > h6{
    color:#182026;
    font-weight:600;
    overflow:hidden;
    text-overflow:ellipsis;
    white-space:nowrap;
    word-wrap:normal;
    line-height:17px;
    margin:0;
    padding:10px 7px 0 1px; }
    .bp3-dark .bp3-menu-header > h6{
      color:#f5f8fa; }
  .bp3-menu-header:first-of-type > h6{
    padding-top:0; }
  .bp3-large .bp3-menu-header > h6{
    font-size:18px;
    padding-bottom:5px;
    padding-top:15px; }
  .bp3-large .bp3-menu-header:first-of-type > h6{
    padding-top:0; }

.bp3-dark .bp3-menu{
  background:#30404d;
  color:#f5f8fa; }

.bp3-dark .bp3-menu-item{ }
  .bp3-dark .bp3-menu-item.bp3-intent-primary{
    color:#48aff0; }
    .bp3-dark .bp3-menu-item.bp3-intent-primary .bp3-icon{
      color:inherit; }
    .bp3-dark .bp3-menu-item.bp3-intent-primary::before, .bp3-dark .bp3-menu-item.bp3-intent-primary::after,
    .bp3-dark .bp3-menu-item.bp3-intent-primary .bp3-menu-item-label{
      color:#48aff0; }
    .bp3-dark .bp3-menu-item.bp3-intent-primary:hover, .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-primary.bp3-menu-item, .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-primary.bp3-menu-item, .bp3-dark .bp3-menu-item.bp3-intent-primary.bp3-active{
      background-color:#137cbd; }
    .bp3-dark .bp3-menu-item.bp3-intent-primary:active{
      background-color:#106ba3; }
    .bp3-dark .bp3-menu-item.bp3-intent-primary:hover, .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-primary.bp3-menu-item, .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-primary.bp3-menu-item, .bp3-dark .bp3-menu-item.bp3-intent-primary:hover::before, .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-primary.bp3-menu-item::before, .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-primary.bp3-menu-item::before, .bp3-dark .bp3-menu-item.bp3-intent-primary:hover::after, .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-primary.bp3-menu-item::after, .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-primary.bp3-menu-item::after,
    .bp3-dark .bp3-menu-item.bp3-intent-primary:hover .bp3-menu-item-label,
    .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-primary.bp3-menu-item .bp3-menu-item-label,
    .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-primary.bp3-menu-item .bp3-menu-item-label, .bp3-dark .bp3-menu-item.bp3-intent-primary:active, .bp3-dark .bp3-menu-item.bp3-intent-primary:active::before, .bp3-dark .bp3-menu-item.bp3-intent-primary:active::after,
    .bp3-dark .bp3-menu-item.bp3-intent-primary:active .bp3-menu-item-label, .bp3-dark .bp3-menu-item.bp3-intent-primary.bp3-active, .bp3-dark .bp3-menu-item.bp3-intent-primary.bp3-active::before, .bp3-dark .bp3-menu-item.bp3-intent-primary.bp3-active::after,
    .bp3-dark .bp3-menu-item.bp3-intent-primary.bp3-active .bp3-menu-item-label{
      color:#ffffff; }
  .bp3-dark .bp3-menu-item.bp3-intent-success{
    color:#3dcc91; }
    .bp3-dark .bp3-menu-item.bp3-intent-success .bp3-icon{
      color:inherit; }
    .bp3-dark .bp3-menu-item.bp3-intent-success::before, .bp3-dark .bp3-menu-item.bp3-intent-success::after,
    .bp3-dark .bp3-menu-item.bp3-intent-success .bp3-menu-item-label{
      color:#3dcc91; }
    .bp3-dark .bp3-menu-item.bp3-intent-success:hover, .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-success.bp3-menu-item, .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-success.bp3-menu-item, .bp3-dark .bp3-menu-item.bp3-intent-success.bp3-active{
      background-color:#0f9960; }
    .bp3-dark .bp3-menu-item.bp3-intent-success:active{
      background-color:#0d8050; }
    .bp3-dark .bp3-menu-item.bp3-intent-success:hover, .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-success.bp3-menu-item, .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-success.bp3-menu-item, .bp3-dark .bp3-menu-item.bp3-intent-success:hover::before, .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-success.bp3-menu-item::before, .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-success.bp3-menu-item::before, .bp3-dark .bp3-menu-item.bp3-intent-success:hover::after, .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-success.bp3-menu-item::after, .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-success.bp3-menu-item::after,
    .bp3-dark .bp3-menu-item.bp3-intent-success:hover .bp3-menu-item-label,
    .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-success.bp3-menu-item .bp3-menu-item-label,
    .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-success.bp3-menu-item .bp3-menu-item-label, .bp3-dark .bp3-menu-item.bp3-intent-success:active, .bp3-dark .bp3-menu-item.bp3-intent-success:active::before, .bp3-dark .bp3-menu-item.bp3-intent-success:active::after,
    .bp3-dark .bp3-menu-item.bp3-intent-success:active .bp3-menu-item-label, .bp3-dark .bp3-menu-item.bp3-intent-success.bp3-active, .bp3-dark .bp3-menu-item.bp3-intent-success.bp3-active::before, .bp3-dark .bp3-menu-item.bp3-intent-success.bp3-active::after,
    .bp3-dark .bp3-menu-item.bp3-intent-success.bp3-active .bp3-menu-item-label{
      color:#ffffff; }
  .bp3-dark .bp3-menu-item.bp3-intent-warning{
    color:#ffb366; }
    .bp3-dark .bp3-menu-item.bp3-intent-warning .bp3-icon{
      color:inherit; }
    .bp3-dark .bp3-menu-item.bp3-intent-warning::before, .bp3-dark .bp3-menu-item.bp3-intent-warning::after,
    .bp3-dark .bp3-menu-item.bp3-intent-warning .bp3-menu-item-label{
      color:#ffb366; }
    .bp3-dark .bp3-menu-item.bp3-intent-warning:hover, .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-warning.bp3-menu-item, .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-warning.bp3-menu-item, .bp3-dark .bp3-menu-item.bp3-intent-warning.bp3-active{
      background-color:#d9822b; }
    .bp3-dark .bp3-menu-item.bp3-intent-warning:active{
      background-color:#bf7326; }
    .bp3-dark .bp3-menu-item.bp3-intent-warning:hover, .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-warning.bp3-menu-item, .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-warning.bp3-menu-item, .bp3-dark .bp3-menu-item.bp3-intent-warning:hover::before, .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-warning.bp3-menu-item::before, .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-warning.bp3-menu-item::before, .bp3-dark .bp3-menu-item.bp3-intent-warning:hover::after, .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-warning.bp3-menu-item::after, .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-warning.bp3-menu-item::after,
    .bp3-dark .bp3-menu-item.bp3-intent-warning:hover .bp3-menu-item-label,
    .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-warning.bp3-menu-item .bp3-menu-item-label,
    .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-warning.bp3-menu-item .bp3-menu-item-label, .bp3-dark .bp3-menu-item.bp3-intent-warning:active, .bp3-dark .bp3-menu-item.bp3-intent-warning:active::before, .bp3-dark .bp3-menu-item.bp3-intent-warning:active::after,
    .bp3-dark .bp3-menu-item.bp3-intent-warning:active .bp3-menu-item-label, .bp3-dark .bp3-menu-item.bp3-intent-warning.bp3-active, .bp3-dark .bp3-menu-item.bp3-intent-warning.bp3-active::before, .bp3-dark .bp3-menu-item.bp3-intent-warning.bp3-active::after,
    .bp3-dark .bp3-menu-item.bp3-intent-warning.bp3-active .bp3-menu-item-label{
      color:#ffffff; }
  .bp3-dark .bp3-menu-item.bp3-intent-danger{
    color:#ff7373; }
    .bp3-dark .bp3-menu-item.bp3-intent-danger .bp3-icon{
      color:inherit; }
    .bp3-dark .bp3-menu-item.bp3-intent-danger::before, .bp3-dark .bp3-menu-item.bp3-intent-danger::after,
    .bp3-dark .bp3-menu-item.bp3-intent-danger .bp3-menu-item-label{
      color:#ff7373; }
    .bp3-dark .bp3-menu-item.bp3-intent-danger:hover, .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-danger.bp3-menu-item, .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-danger.bp3-menu-item, .bp3-dark .bp3-menu-item.bp3-intent-danger.bp3-active{
      background-color:#db3737; }
    .bp3-dark .bp3-menu-item.bp3-intent-danger:active{
      background-color:#c23030; }
    .bp3-dark .bp3-menu-item.bp3-intent-danger:hover, .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-danger.bp3-menu-item, .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-danger.bp3-menu-item, .bp3-dark .bp3-menu-item.bp3-intent-danger:hover::before, .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-danger.bp3-menu-item::before, .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-danger.bp3-menu-item::before, .bp3-dark .bp3-menu-item.bp3-intent-danger:hover::after, .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-danger.bp3-menu-item::after, .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-danger.bp3-menu-item::after,
    .bp3-dark .bp3-menu-item.bp3-intent-danger:hover .bp3-menu-item-label,
    .bp3-dark .bp3-submenu .bp3-popover-target.bp3-popover-open > .bp3-intent-danger.bp3-menu-item .bp3-menu-item-label,
    .bp3-submenu .bp3-dark .bp3-popover-target.bp3-popover-open > .bp3-intent-danger.bp3-menu-item .bp3-menu-item-label, .bp3-dark .bp3-menu-item.bp3-intent-danger:active, .bp3-dark .bp3-menu-item.bp3-intent-danger:active::before, .bp3-dark .bp3-menu-item.bp3-intent-danger:active::after,
    .bp3-dark .bp3-menu-item.bp3-intent-danger:active .bp3-menu-item-label, .bp3-dark .bp3-menu-item.bp3-intent-danger.bp3-active, .bp3-dark .bp3-menu-item.bp3-intent-danger.bp3-active::before, .bp3-dark .bp3-menu-item.bp3-intent-danger.bp3-active::after,
    .bp3-dark .bp3-menu-item.bp3-intent-danger.bp3-active .bp3-menu-item-label{
      color:#ffffff; }
  .bp3-dark .bp3-menu-item::before,
  .bp3-dark .bp3-menu-item > .bp3-icon{
    color:#a7b6c2; }
  .bp3-dark .bp3-menu-item .bp3-menu-item-label{
    color:#a7b6c2; }
  .bp3-dark .bp3-menu-item.bp3-active, .bp3-dark .bp3-menu-item:active{
    background-color:rgba(138, 155, 168, 0.3); }
  .bp3-dark .bp3-menu-item.bp3-disabled{
    color:rgba(167, 182, 194, 0.6) !important; }
    .bp3-dark .bp3-menu-item.bp3-disabled::before,
    .bp3-dark .bp3-menu-item.bp3-disabled > .bp3-icon,
    .bp3-dark .bp3-menu-item.bp3-disabled .bp3-menu-item-label{
      color:rgba(167, 182, 194, 0.6) !important; }

.bp3-dark .bp3-menu-divider,
.bp3-dark .bp3-menu-header{
  border-color:rgba(255, 255, 255, 0.15); }

.bp3-dark .bp3-menu-header > h6{
  color:#f5f8fa; }

.bp3-label .bp3-menu{
  margin-top:5px; }
.bp3-navbar{
  background-color:#ffffff;
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.2);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.2);
  height:50px;
  padding:0 15px;
  position:relative;
  width:100%;
  z-index:10; }
  .bp3-navbar.bp3-dark,
  .bp3-dark .bp3-navbar{
    background-color:#394b59; }
  .bp3-navbar.bp3-dark{
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.4);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.4); }
  .bp3-dark .bp3-navbar{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 0 0 rgba(16, 22, 26, 0), 0 1px 1px rgba(16, 22, 26, 0.4); }
  .bp3-navbar.bp3-fixed-top{
    left:0;
    position:fixed;
    right:0;
    top:0; }

.bp3-navbar-heading{
  font-size:16px;
  margin-right:15px; }

.bp3-navbar-group{
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center;
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  height:50px; }
  .bp3-navbar-group.bp3-align-left{
    float:left; }
  .bp3-navbar-group.bp3-align-right{
    float:right; }

.bp3-navbar-divider{
  border-left:1px solid rgba(16, 22, 26, 0.15);
  height:20px;
  margin:0 10px; }
  .bp3-dark .bp3-navbar-divider{
    border-left-color:rgba(255, 255, 255, 0.15); }
.bp3-non-ideal-state{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-orient:vertical;
  -webkit-box-direction:normal;
      -ms-flex-direction:column;
          flex-direction:column;
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center;
  height:100%;
  -webkit-box-pack:center;
      -ms-flex-pack:center;
          justify-content:center;
  text-align:center;
  width:100%; }
  .bp3-non-ideal-state > *{
    -webkit-box-flex:0;
        -ms-flex-positive:0;
            flex-grow:0;
    -ms-flex-negative:0;
        flex-shrink:0; }
  .bp3-non-ideal-state > .bp3-fill{
    -webkit-box-flex:1;
        -ms-flex-positive:1;
            flex-grow:1;
    -ms-flex-negative:1;
        flex-shrink:1; }
  .bp3-non-ideal-state::before,
  .bp3-non-ideal-state > *{
    margin-bottom:20px; }
  .bp3-non-ideal-state:empty::before,
  .bp3-non-ideal-state > :last-child{
    margin-bottom:0; }
  .bp3-non-ideal-state > *{
    max-width:400px; }

.bp3-non-ideal-state-visual{
  color:rgba(92, 112, 128, 0.6);
  font-size:60px; }
  .bp3-dark .bp3-non-ideal-state-visual{
    color:rgba(167, 182, 194, 0.6); }

.bp3-overflow-list{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -ms-flex-wrap:nowrap;
      flex-wrap:nowrap;
  min-width:0; }

.bp3-overflow-list-spacer{
  -ms-flex-negative:1;
      flex-shrink:1;
  width:1px; }

body.bp3-overlay-open{
  overflow:hidden; }

.bp3-overlay{
  bottom:0;
  left:0;
  position:static;
  right:0;
  top:0;
  z-index:20; }
  .bp3-overlay:not(.bp3-overlay-open){
    pointer-events:none; }
  .bp3-overlay.bp3-overlay-container{
    overflow:hidden;
    position:fixed; }
    .bp3-overlay.bp3-overlay-container.bp3-overlay-inline{
      position:absolute; }
  .bp3-overlay.bp3-overlay-scroll-container{
    overflow:auto;
    position:fixed; }
    .bp3-overlay.bp3-overlay-scroll-container.bp3-overlay-inline{
      position:absolute; }
  .bp3-overlay.bp3-overlay-inline{
    display:inline;
    overflow:visible; }

.bp3-overlay-content{
  position:fixed;
  z-index:20; }
  .bp3-overlay-inline .bp3-overlay-content,
  .bp3-overlay-scroll-container .bp3-overlay-content{
    position:absolute; }

.bp3-overlay-backdrop{
  bottom:0;
  left:0;
  position:fixed;
  right:0;
  top:0;
  opacity:1;
  background-color:rgba(16, 22, 26, 0.7);
  overflow:auto;
  -webkit-user-select:none;
     -moz-user-select:none;
      -ms-user-select:none;
          user-select:none;
  z-index:20; }
  .bp3-overlay-backdrop.bp3-overlay-enter, .bp3-overlay-backdrop.bp3-overlay-appear{
    opacity:0; }
  .bp3-overlay-backdrop.bp3-overlay-enter-active, .bp3-overlay-backdrop.bp3-overlay-appear-active{
    opacity:1;
    -webkit-transition-delay:0;
            transition-delay:0;
    -webkit-transition-duration:200ms;
            transition-duration:200ms;
    -webkit-transition-property:opacity;
    transition-property:opacity;
    -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
            transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9); }
  .bp3-overlay-backdrop.bp3-overlay-exit{
    opacity:1; }
  .bp3-overlay-backdrop.bp3-overlay-exit-active{
    opacity:0;
    -webkit-transition-delay:0;
            transition-delay:0;
    -webkit-transition-duration:200ms;
            transition-duration:200ms;
    -webkit-transition-property:opacity;
    transition-property:opacity;
    -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
            transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9); }
  .bp3-overlay-backdrop:focus{
    outline:none; }
  .bp3-overlay-inline .bp3-overlay-backdrop{
    position:absolute; }
.bp3-panel-stack{
  overflow:hidden;
  position:relative; }

.bp3-panel-stack-header{
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center;
  -webkit-box-shadow:0 1px rgba(16, 22, 26, 0.15);
          box-shadow:0 1px rgba(16, 22, 26, 0.15);
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -ms-flex-negative:0;
      flex-shrink:0;
  height:30px;
  z-index:1; }
  .bp3-dark .bp3-panel-stack-header{
    -webkit-box-shadow:0 1px rgba(255, 255, 255, 0.15);
            box-shadow:0 1px rgba(255, 255, 255, 0.15); }
  .bp3-panel-stack-header > span{
    -webkit-box-align:stretch;
        -ms-flex-align:stretch;
            align-items:stretch;
    display:-webkit-box;
    display:-ms-flexbox;
    display:flex;
    -webkit-box-flex:1;
        -ms-flex:1;
            flex:1; }
  .bp3-panel-stack-header .bp3-heading{
    margin:0 5px; }

.bp3-button.bp3-panel-stack-header-back{
  margin-left:5px;
  padding-left:0;
  white-space:nowrap; }
  .bp3-button.bp3-panel-stack-header-back .bp3-icon{
    margin:0 2px; }

.bp3-panel-stack-view{
  bottom:0;
  left:0;
  position:absolute;
  right:0;
  top:0;
  background-color:#ffffff;
  border-right:1px solid rgba(16, 22, 26, 0.15);
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-orient:vertical;
  -webkit-box-direction:normal;
      -ms-flex-direction:column;
          flex-direction:column;
  margin-right:-1px;
  overflow-y:auto;
  z-index:1; }
  .bp3-dark .bp3-panel-stack-view{
    background-color:#30404d; }
  .bp3-panel-stack-view:nth-last-child(n + 4){
    display:none; }

.bp3-panel-stack-push .bp3-panel-stack-enter, .bp3-panel-stack-push .bp3-panel-stack-appear{
  -webkit-transform:translateX(100%);
          transform:translateX(100%);
  opacity:0; }

.bp3-panel-stack-push .bp3-panel-stack-enter-active, .bp3-panel-stack-push .bp3-panel-stack-appear-active{
  -webkit-transform:translate(0%);
          transform:translate(0%);
  opacity:1;
  -webkit-transition-delay:0;
          transition-delay:0;
  -webkit-transition-duration:400ms;
          transition-duration:400ms;
  -webkit-transition-property:opacity, -webkit-transform;
  transition-property:opacity, -webkit-transform;
  transition-property:transform, opacity;
  transition-property:transform, opacity, -webkit-transform;
  -webkit-transition-timing-function:ease;
          transition-timing-function:ease; }

.bp3-panel-stack-push .bp3-panel-stack-exit{
  -webkit-transform:translate(0%);
          transform:translate(0%);
  opacity:1; }

.bp3-panel-stack-push .bp3-panel-stack-exit-active{
  -webkit-transform:translateX(-50%);
          transform:translateX(-50%);
  opacity:0;
  -webkit-transition-delay:0;
          transition-delay:0;
  -webkit-transition-duration:400ms;
          transition-duration:400ms;
  -webkit-transition-property:opacity, -webkit-transform;
  transition-property:opacity, -webkit-transform;
  transition-property:transform, opacity;
  transition-property:transform, opacity, -webkit-transform;
  -webkit-transition-timing-function:ease;
          transition-timing-function:ease; }

.bp3-panel-stack-pop .bp3-panel-stack-enter, .bp3-panel-stack-pop .bp3-panel-stack-appear{
  -webkit-transform:translateX(-50%);
          transform:translateX(-50%);
  opacity:0; }

.bp3-panel-stack-pop .bp3-panel-stack-enter-active, .bp3-panel-stack-pop .bp3-panel-stack-appear-active{
  -webkit-transform:translate(0%);
          transform:translate(0%);
  opacity:1;
  -webkit-transition-delay:0;
          transition-delay:0;
  -webkit-transition-duration:400ms;
          transition-duration:400ms;
  -webkit-transition-property:opacity, -webkit-transform;
  transition-property:opacity, -webkit-transform;
  transition-property:transform, opacity;
  transition-property:transform, opacity, -webkit-transform;
  -webkit-transition-timing-function:ease;
          transition-timing-function:ease; }

.bp3-panel-stack-pop .bp3-panel-stack-exit{
  -webkit-transform:translate(0%);
          transform:translate(0%);
  opacity:1; }

.bp3-panel-stack-pop .bp3-panel-stack-exit-active{
  -webkit-transform:translateX(100%);
          transform:translateX(100%);
  opacity:0;
  -webkit-transition-delay:0;
          transition-delay:0;
  -webkit-transition-duration:400ms;
          transition-duration:400ms;
  -webkit-transition-property:opacity, -webkit-transform;
  transition-property:opacity, -webkit-transform;
  transition-property:transform, opacity;
  transition-property:transform, opacity, -webkit-transform;
  -webkit-transition-timing-function:ease;
          transition-timing-function:ease; }
.bp3-panel-stack2{
  overflow:hidden;
  position:relative; }

.bp3-panel-stack2-header{
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center;
  -webkit-box-shadow:0 1px rgba(16, 22, 26, 0.15);
          box-shadow:0 1px rgba(16, 22, 26, 0.15);
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -ms-flex-negative:0;
      flex-shrink:0;
  height:30px;
  z-index:1; }
  .bp3-dark .bp3-panel-stack2-header{
    -webkit-box-shadow:0 1px rgba(255, 255, 255, 0.15);
            box-shadow:0 1px rgba(255, 255, 255, 0.15); }
  .bp3-panel-stack2-header > span{
    -webkit-box-align:stretch;
        -ms-flex-align:stretch;
            align-items:stretch;
    display:-webkit-box;
    display:-ms-flexbox;
    display:flex;
    -webkit-box-flex:1;
        -ms-flex:1;
            flex:1; }
  .bp3-panel-stack2-header .bp3-heading{
    margin:0 5px; }

.bp3-button.bp3-panel-stack2-header-back{
  margin-left:5px;
  padding-left:0;
  white-space:nowrap; }
  .bp3-button.bp3-panel-stack2-header-back .bp3-icon{
    margin:0 2px; }

.bp3-panel-stack2-view{
  bottom:0;
  left:0;
  position:absolute;
  right:0;
  top:0;
  background-color:#ffffff;
  border-right:1px solid rgba(16, 22, 26, 0.15);
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-orient:vertical;
  -webkit-box-direction:normal;
      -ms-flex-direction:column;
          flex-direction:column;
  margin-right:-1px;
  overflow-y:auto;
  z-index:1; }
  .bp3-dark .bp3-panel-stack2-view{
    background-color:#30404d; }
  .bp3-panel-stack2-view:nth-last-child(n + 4){
    display:none; }

.bp3-panel-stack2-push .bp3-panel-stack2-enter, .bp3-panel-stack2-push .bp3-panel-stack2-appear{
  -webkit-transform:translateX(100%);
          transform:translateX(100%);
  opacity:0; }

.bp3-panel-stack2-push .bp3-panel-stack2-enter-active, .bp3-panel-stack2-push .bp3-panel-stack2-appear-active{
  -webkit-transform:translate(0%);
          transform:translate(0%);
  opacity:1;
  -webkit-transition-delay:0;
          transition-delay:0;
  -webkit-transition-duration:400ms;
          transition-duration:400ms;
  -webkit-transition-property:opacity, -webkit-transform;
  transition-property:opacity, -webkit-transform;
  transition-property:transform, opacity;
  transition-property:transform, opacity, -webkit-transform;
  -webkit-transition-timing-function:ease;
          transition-timing-function:ease; }

.bp3-panel-stack2-push .bp3-panel-stack2-exit{
  -webkit-transform:translate(0%);
          transform:translate(0%);
  opacity:1; }

.bp3-panel-stack2-push .bp3-panel-stack2-exit-active{
  -webkit-transform:translateX(-50%);
          transform:translateX(-50%);
  opacity:0;
  -webkit-transition-delay:0;
          transition-delay:0;
  -webkit-transition-duration:400ms;
          transition-duration:400ms;
  -webkit-transition-property:opacity, -webkit-transform;
  transition-property:opacity, -webkit-transform;
  transition-property:transform, opacity;
  transition-property:transform, opacity, -webkit-transform;
  -webkit-transition-timing-function:ease;
          transition-timing-function:ease; }

.bp3-panel-stack2-pop .bp3-panel-stack2-enter, .bp3-panel-stack2-pop .bp3-panel-stack2-appear{
  -webkit-transform:translateX(-50%);
          transform:translateX(-50%);
  opacity:0; }

.bp3-panel-stack2-pop .bp3-panel-stack2-enter-active, .bp3-panel-stack2-pop .bp3-panel-stack2-appear-active{
  -webkit-transform:translate(0%);
          transform:translate(0%);
  opacity:1;
  -webkit-transition-delay:0;
          transition-delay:0;
  -webkit-transition-duration:400ms;
          transition-duration:400ms;
  -webkit-transition-property:opacity, -webkit-transform;
  transition-property:opacity, -webkit-transform;
  transition-property:transform, opacity;
  transition-property:transform, opacity, -webkit-transform;
  -webkit-transition-timing-function:ease;
          transition-timing-function:ease; }

.bp3-panel-stack2-pop .bp3-panel-stack2-exit{
  -webkit-transform:translate(0%);
          transform:translate(0%);
  opacity:1; }

.bp3-panel-stack2-pop .bp3-panel-stack2-exit-active{
  -webkit-transform:translateX(100%);
          transform:translateX(100%);
  opacity:0;
  -webkit-transition-delay:0;
          transition-delay:0;
  -webkit-transition-duration:400ms;
          transition-duration:400ms;
  -webkit-transition-property:opacity, -webkit-transform;
  transition-property:opacity, -webkit-transform;
  transition-property:transform, opacity;
  transition-property:transform, opacity, -webkit-transform;
  -webkit-transition-timing-function:ease;
          transition-timing-function:ease; }
.bp3-popover{
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 2px 4px rgba(16, 22, 26, 0.2), 0 8px 24px rgba(16, 22, 26, 0.2);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 2px 4px rgba(16, 22, 26, 0.2), 0 8px 24px rgba(16, 22, 26, 0.2);
  -webkit-transform:scale(1);
          transform:scale(1);
  border-radius:3px;
  display:inline-block;
  z-index:20; }
  .bp3-popover .bp3-popover-arrow{
    height:30px;
    position:absolute;
    width:30px; }
    .bp3-popover .bp3-popover-arrow::before{
      height:20px;
      margin:5px;
      width:20px; }
  .bp3-tether-element-attached-bottom.bp3-tether-target-attached-top > .bp3-popover{
    margin-bottom:17px;
    margin-top:-17px; }
    .bp3-tether-element-attached-bottom.bp3-tether-target-attached-top > .bp3-popover > .bp3-popover-arrow{
      bottom:-11px; }
      .bp3-tether-element-attached-bottom.bp3-tether-target-attached-top > .bp3-popover > .bp3-popover-arrow svg{
        -webkit-transform:rotate(-90deg);
                transform:rotate(-90deg); }
  .bp3-tether-element-attached-left.bp3-tether-target-attached-right > .bp3-popover{
    margin-left:17px; }
    .bp3-tether-element-attached-left.bp3-tether-target-attached-right > .bp3-popover > .bp3-popover-arrow{
      left:-11px; }
      .bp3-tether-element-attached-left.bp3-tether-target-attached-right > .bp3-popover > .bp3-popover-arrow svg{
        -webkit-transform:rotate(0);
                transform:rotate(0); }
  .bp3-tether-element-attached-top.bp3-tether-target-attached-bottom > .bp3-popover{
    margin-top:17px; }
    .bp3-tether-element-attached-top.bp3-tether-target-attached-bottom > .bp3-popover > .bp3-popover-arrow{
      top:-11px; }
      .bp3-tether-element-attached-top.bp3-tether-target-attached-bottom > .bp3-popover > .bp3-popover-arrow svg{
        -webkit-transform:rotate(90deg);
                transform:rotate(90deg); }
  .bp3-tether-element-attached-right.bp3-tether-target-attached-left > .bp3-popover{
    margin-left:-17px;
    margin-right:17px; }
    .bp3-tether-element-attached-right.bp3-tether-target-attached-left > .bp3-popover > .bp3-popover-arrow{
      right:-11px; }
      .bp3-tether-element-attached-right.bp3-tether-target-attached-left > .bp3-popover > .bp3-popover-arrow svg{
        -webkit-transform:rotate(180deg);
                transform:rotate(180deg); }
  .bp3-tether-element-attached-middle > .bp3-popover > .bp3-popover-arrow{
    top:50%;
    -webkit-transform:translateY(-50%);
            transform:translateY(-50%); }
  .bp3-tether-element-attached-center > .bp3-popover > .bp3-popover-arrow{
    right:50%;
    -webkit-transform:translateX(50%);
            transform:translateX(50%); }
  .bp3-tether-element-attached-top.bp3-tether-target-attached-top > .bp3-popover > .bp3-popover-arrow{
    top:-0.3934px; }
  .bp3-tether-element-attached-right.bp3-tether-target-attached-right > .bp3-popover > .bp3-popover-arrow{
    right:-0.3934px; }
  .bp3-tether-element-attached-left.bp3-tether-target-attached-left > .bp3-popover > .bp3-popover-arrow{
    left:-0.3934px; }
  .bp3-tether-element-attached-bottom.bp3-tether-target-attached-bottom > .bp3-popover > .bp3-popover-arrow{
    bottom:-0.3934px; }
  .bp3-tether-element-attached-top.bp3-tether-element-attached-left > .bp3-popover{
    -webkit-transform-origin:top left;
            transform-origin:top left; }
  .bp3-tether-element-attached-top.bp3-tether-element-attached-center > .bp3-popover{
    -webkit-transform-origin:top center;
            transform-origin:top center; }
  .bp3-tether-element-attached-top.bp3-tether-element-attached-right > .bp3-popover{
    -webkit-transform-origin:top right;
            transform-origin:top right; }
  .bp3-tether-element-attached-middle.bp3-tether-element-attached-left > .bp3-popover{
    -webkit-transform-origin:center left;
            transform-origin:center left; }
  .bp3-tether-element-attached-middle.bp3-tether-element-attached-center > .bp3-popover{
    -webkit-transform-origin:center center;
            transform-origin:center center; }
  .bp3-tether-element-attached-middle.bp3-tether-element-attached-right > .bp3-popover{
    -webkit-transform-origin:center right;
            transform-origin:center right; }
  .bp3-tether-element-attached-bottom.bp3-tether-element-attached-left > .bp3-popover{
    -webkit-transform-origin:bottom left;
            transform-origin:bottom left; }
  .bp3-tether-element-attached-bottom.bp3-tether-element-attached-center > .bp3-popover{
    -webkit-transform-origin:bottom center;
            transform-origin:bottom center; }
  .bp3-tether-element-attached-bottom.bp3-tether-element-attached-right > .bp3-popover{
    -webkit-transform-origin:bottom right;
            transform-origin:bottom right; }
  .bp3-popover .bp3-popover-content{
    background:#ffffff;
    color:inherit; }
  .bp3-popover .bp3-popover-arrow::before{
    -webkit-box-shadow:1px 1px 6px rgba(16, 22, 26, 0.2);
            box-shadow:1px 1px 6px rgba(16, 22, 26, 0.2); }
  .bp3-popover .bp3-popover-arrow-border{
    fill:#10161a;
    fill-opacity:0.1; }
  .bp3-popover .bp3-popover-arrow-fill{
    fill:#ffffff; }
  .bp3-popover-enter > .bp3-popover, .bp3-popover-appear > .bp3-popover{
    -webkit-transform:scale(0.3);
            transform:scale(0.3); }
  .bp3-popover-enter-active > .bp3-popover, .bp3-popover-appear-active > .bp3-popover{
    -webkit-transform:scale(1);
            transform:scale(1);
    -webkit-transition-delay:0;
            transition-delay:0;
    -webkit-transition-duration:300ms;
            transition-duration:300ms;
    -webkit-transition-property:-webkit-transform;
    transition-property:-webkit-transform;
    transition-property:transform;
    transition-property:transform, -webkit-transform;
    -webkit-transition-timing-function:cubic-bezier(0.54, 1.12, 0.38, 1.11);
            transition-timing-function:cubic-bezier(0.54, 1.12, 0.38, 1.11); }
  .bp3-popover-exit > .bp3-popover{
    -webkit-transform:scale(1);
            transform:scale(1); }
  .bp3-popover-exit-active > .bp3-popover{
    -webkit-transform:scale(0.3);
            transform:scale(0.3);
    -webkit-transition-delay:0;
            transition-delay:0;
    -webkit-transition-duration:300ms;
            transition-duration:300ms;
    -webkit-transition-property:-webkit-transform;
    transition-property:-webkit-transform;
    transition-property:transform;
    transition-property:transform, -webkit-transform;
    -webkit-transition-timing-function:cubic-bezier(0.54, 1.12, 0.38, 1.11);
            transition-timing-function:cubic-bezier(0.54, 1.12, 0.38, 1.11); }
  .bp3-popover .bp3-popover-content{
    border-radius:3px;
    position:relative; }
  .bp3-popover.bp3-popover-content-sizing .bp3-popover-content{
    max-width:350px;
    padding:20px; }
  .bp3-popover-target + .bp3-overlay .bp3-popover.bp3-popover-content-sizing{
    width:350px; }
  .bp3-popover.bp3-minimal{
    margin:0 !important; }
    .bp3-popover.bp3-minimal .bp3-popover-arrow{
      display:none; }
    .bp3-popover.bp3-minimal.bp3-popover{
      -webkit-transform:scale(1);
              transform:scale(1); }
      .bp3-popover-enter > .bp3-popover.bp3-minimal.bp3-popover, .bp3-popover-appear > .bp3-popover.bp3-minimal.bp3-popover{
        -webkit-transform:scale(1);
                transform:scale(1); }
      .bp3-popover-enter-active > .bp3-popover.bp3-minimal.bp3-popover, .bp3-popover-appear-active > .bp3-popover.bp3-minimal.bp3-popover{
        -webkit-transform:scale(1);
                transform:scale(1);
        -webkit-transition-delay:0;
                transition-delay:0;
        -webkit-transition-duration:100ms;
                transition-duration:100ms;
        -webkit-transition-property:-webkit-transform;
        transition-property:-webkit-transform;
        transition-property:transform;
        transition-property:transform, -webkit-transform;
        -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
                transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9); }
      .bp3-popover-exit > .bp3-popover.bp3-minimal.bp3-popover{
        -webkit-transform:scale(1);
                transform:scale(1); }
      .bp3-popover-exit-active > .bp3-popover.bp3-minimal.bp3-popover{
        -webkit-transform:scale(1);
                transform:scale(1);
        -webkit-transition-delay:0;
                transition-delay:0;
        -webkit-transition-duration:100ms;
                transition-duration:100ms;
        -webkit-transition-property:-webkit-transform;
        transition-property:-webkit-transform;
        transition-property:transform;
        transition-property:transform, -webkit-transform;
        -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
                transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9); }
  .bp3-popover.bp3-dark,
  .bp3-dark .bp3-popover{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 2px 4px rgba(16, 22, 26, 0.4), 0 8px 24px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 2px 4px rgba(16, 22, 26, 0.4), 0 8px 24px rgba(16, 22, 26, 0.4); }
    .bp3-popover.bp3-dark .bp3-popover-content,
    .bp3-dark .bp3-popover .bp3-popover-content{
      background:#30404d;
      color:inherit; }
    .bp3-popover.bp3-dark .bp3-popover-arrow::before,
    .bp3-dark .bp3-popover .bp3-popover-arrow::before{
      -webkit-box-shadow:1px 1px 6px rgba(16, 22, 26, 0.4);
              box-shadow:1px 1px 6px rgba(16, 22, 26, 0.4); }
    .bp3-popover.bp3-dark .bp3-popover-arrow-border,
    .bp3-dark .bp3-popover .bp3-popover-arrow-border{
      fill:#10161a;
      fill-opacity:0.2; }
    .bp3-popover.bp3-dark .bp3-popover-arrow-fill,
    .bp3-dark .bp3-popover .bp3-popover-arrow-fill{
      fill:#30404d; }

.bp3-popover-arrow::before{
  border-radius:2px;
  content:"";
  display:block;
  position:absolute;
  -webkit-transform:rotate(45deg);
          transform:rotate(45deg); }

.bp3-tether-pinned .bp3-popover-arrow{
  display:none; }

.bp3-popover-backdrop{
  background:rgba(255, 255, 255, 0); }

.bp3-transition-container{
  opacity:1;
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  z-index:20; }
  .bp3-transition-container.bp3-popover-enter, .bp3-transition-container.bp3-popover-appear{
    opacity:0; }
  .bp3-transition-container.bp3-popover-enter-active, .bp3-transition-container.bp3-popover-appear-active{
    opacity:1;
    -webkit-transition-delay:0;
            transition-delay:0;
    -webkit-transition-duration:100ms;
            transition-duration:100ms;
    -webkit-transition-property:opacity;
    transition-property:opacity;
    -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
            transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9); }
  .bp3-transition-container.bp3-popover-exit{
    opacity:1; }
  .bp3-transition-container.bp3-popover-exit-active{
    opacity:0;
    -webkit-transition-delay:0;
            transition-delay:0;
    -webkit-transition-duration:100ms;
            transition-duration:100ms;
    -webkit-transition-property:opacity;
    transition-property:opacity;
    -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
            transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9); }
  .bp3-transition-container:focus{
    outline:none; }
  .bp3-transition-container.bp3-popover-leave .bp3-popover-content{
    pointer-events:none; }
  .bp3-transition-container[data-x-out-of-boundaries]{
    display:none; }

span.bp3-popover-target{
  display:inline-block; }

.bp3-popover-wrapper.bp3-fill{
  width:100%; }

.bp3-portal{
  left:0;
  position:absolute;
  right:0;
  top:0; }
@-webkit-keyframes linear-progress-bar-stripes{
  from{
    background-position:0 0; }
  to{
    background-position:30px 0; } }
@keyframes linear-progress-bar-stripes{
  from{
    background-position:0 0; }
  to{
    background-position:30px 0; } }

.bp3-progress-bar{
  background:rgba(92, 112, 128, 0.2);
  border-radius:40px;
  display:block;
  height:8px;
  overflow:hidden;
  position:relative;
  width:100%; }
  .bp3-progress-bar .bp3-progress-meter{
    background:linear-gradient(-45deg, rgba(255, 255, 255, 0.2) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.2) 50%, rgba(255, 255, 255, 0.2) 75%, transparent 75%);
    background-color:rgba(92, 112, 128, 0.8);
    background-size:30px 30px;
    border-radius:40px;
    height:100%;
    position:absolute;
    -webkit-transition:width 200ms cubic-bezier(0.4, 1, 0.75, 0.9);
    transition:width 200ms cubic-bezier(0.4, 1, 0.75, 0.9);
    width:100%; }
  .bp3-progress-bar:not(.bp3-no-animation):not(.bp3-no-stripes) .bp3-progress-meter{
    animation:linear-progress-bar-stripes 300ms linear infinite reverse; }
  .bp3-progress-bar.bp3-no-stripes .bp3-progress-meter{
    background-image:none; }

.bp3-dark .bp3-progress-bar{
  background:rgba(16, 22, 26, 0.5); }
  .bp3-dark .bp3-progress-bar .bp3-progress-meter{
    background-color:#8a9ba8; }

.bp3-progress-bar.bp3-intent-primary .bp3-progress-meter{
  background-color:#137cbd; }

.bp3-progress-bar.bp3-intent-success .bp3-progress-meter{
  background-color:#0f9960; }

.bp3-progress-bar.bp3-intent-warning .bp3-progress-meter{
  background-color:#d9822b; }

.bp3-progress-bar.bp3-intent-danger .bp3-progress-meter{
  background-color:#db3737; }
@-webkit-keyframes skeleton-glow{
  from{
    background:rgba(206, 217, 224, 0.2);
    border-color:rgba(206, 217, 224, 0.2); }
  to{
    background:rgba(92, 112, 128, 0.2);
    border-color:rgba(92, 112, 128, 0.2); } }
@keyframes skeleton-glow{
  from{
    background:rgba(206, 217, 224, 0.2);
    border-color:rgba(206, 217, 224, 0.2); }
  to{
    background:rgba(92, 112, 128, 0.2);
    border-color:rgba(92, 112, 128, 0.2); } }
.bp3-skeleton{
  -webkit-animation:1000ms linear infinite alternate skeleton-glow;
          animation:1000ms linear infinite alternate skeleton-glow;
  background:rgba(206, 217, 224, 0.2);
  background-clip:padding-box !important;
  border-color:rgba(206, 217, 224, 0.2) !important;
  border-radius:2px;
  -webkit-box-shadow:none !important;
          box-shadow:none !important;
  color:transparent !important;
  cursor:default;
  pointer-events:none;
  -webkit-user-select:none;
     -moz-user-select:none;
      -ms-user-select:none;
          user-select:none; }
  .bp3-skeleton::before, .bp3-skeleton::after,
  .bp3-skeleton *{
    visibility:hidden !important; }
.bp3-slider{
  height:40px;
  min-width:150px;
  width:100%;
  cursor:default;
  outline:none;
  position:relative;
  -webkit-user-select:none;
     -moz-user-select:none;
      -ms-user-select:none;
          user-select:none; }
  .bp3-slider:hover{
    cursor:pointer; }
  .bp3-slider:active{
    cursor:-webkit-grabbing;
    cursor:grabbing; }
  .bp3-slider.bp3-disabled{
    cursor:not-allowed;
    opacity:0.5; }
  .bp3-slider.bp3-slider-unlabeled{
    height:16px; }

.bp3-slider-track,
.bp3-slider-progress{
  height:6px;
  left:0;
  right:0;
  top:5px;
  position:absolute; }

.bp3-slider-track{
  border-radius:3px;
  overflow:hidden; }

.bp3-slider-progress{
  background:rgba(92, 112, 128, 0.2); }
  .bp3-dark .bp3-slider-progress{
    background:rgba(16, 22, 26, 0.5); }
  .bp3-slider-progress.bp3-intent-primary{
    background-color:#137cbd; }
  .bp3-slider-progress.bp3-intent-success{
    background-color:#0f9960; }
  .bp3-slider-progress.bp3-intent-warning{
    background-color:#d9822b; }
  .bp3-slider-progress.bp3-intent-danger{
    background-color:#db3737; }

.bp3-slider-handle{
  background-color:#f5f8fa;
  background-image:-webkit-gradient(linear, left top, left bottom, from(rgba(255, 255, 255, 0.8)), to(rgba(255, 255, 255, 0)));
  background-image:linear-gradient(to bottom, rgba(255, 255, 255, 0.8), rgba(255, 255, 255, 0));
  -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
          box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
  color:#182026;
  border-radius:3px;
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 1px 1px rgba(16, 22, 26, 0.2);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 1px 1px rgba(16, 22, 26, 0.2);
  cursor:pointer;
  height:16px;
  left:0;
  position:absolute;
  top:0;
  width:16px; }
  .bp3-slider-handle:hover{
    background-clip:padding-box;
    background-color:#ebf1f5;
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1); }
  .bp3-slider-handle:active, .bp3-slider-handle.bp3-active{
    background-color:#d8e1e8;
    background-image:none;
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 1px 2px rgba(16, 22, 26, 0.2);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 1px 2px rgba(16, 22, 26, 0.2); }
  .bp3-slider-handle:disabled, .bp3-slider-handle.bp3-disabled{
    background-color:rgba(206, 217, 224, 0.5);
    background-image:none;
    -webkit-box-shadow:none;
            box-shadow:none;
    color:rgba(92, 112, 128, 0.6);
    cursor:not-allowed;
    outline:none; }
    .bp3-slider-handle:disabled.bp3-active, .bp3-slider-handle:disabled.bp3-active:hover, .bp3-slider-handle.bp3-disabled.bp3-active, .bp3-slider-handle.bp3-disabled.bp3-active:hover{
      background:rgba(206, 217, 224, 0.7); }
  .bp3-slider-handle:focus{
    z-index:1; }
  .bp3-slider-handle:hover{
    background-clip:padding-box;
    background-color:#ebf1f5;
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 -1px 0 rgba(16, 22, 26, 0.1);
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 1px 1px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 1px 1px rgba(16, 22, 26, 0.2);
    cursor:-webkit-grab;
    cursor:grab;
    z-index:2; }
  .bp3-slider-handle.bp3-active{
    background-color:#d8e1e8;
    background-image:none;
    -webkit-box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 1px 2px rgba(16, 22, 26, 0.2);
            box-shadow:inset 0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 1px 2px rgba(16, 22, 26, 0.2);
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 1px 1px rgba(16, 22, 26, 0.1);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), inset 0 1px 1px rgba(16, 22, 26, 0.1);
    cursor:-webkit-grabbing;
    cursor:grabbing; }
  .bp3-disabled .bp3-slider-handle{
    background:#bfccd6;
    -webkit-box-shadow:none;
            box-shadow:none;
    pointer-events:none; }
  .bp3-dark .bp3-slider-handle{
    background-color:#394b59;
    background-image:-webkit-gradient(linear, left top, left bottom, from(rgba(255, 255, 255, 0.05)), to(rgba(255, 255, 255, 0)));
    background-image:linear-gradient(to bottom, rgba(255, 255, 255, 0.05), rgba(255, 255, 255, 0));
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
    color:#f5f8fa; }
    .bp3-dark .bp3-slider-handle:hover, .bp3-dark .bp3-slider-handle:active, .bp3-dark .bp3-slider-handle.bp3-active{
      color:#f5f8fa; }
    .bp3-dark .bp3-slider-handle:hover{
      background-color:#30404d;
      -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 1px rgba(16, 22, 26, 0.4); }
    .bp3-dark .bp3-slider-handle:active, .bp3-dark .bp3-slider-handle.bp3-active{
      background-color:#202b33;
      background-image:none;
      -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.6), inset 0 1px 2px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px rgba(16, 22, 26, 0.6), inset 0 1px 2px rgba(16, 22, 26, 0.2); }
    .bp3-dark .bp3-slider-handle:disabled, .bp3-dark .bp3-slider-handle.bp3-disabled{
      background-color:rgba(57, 75, 89, 0.5);
      background-image:none;
      -webkit-box-shadow:none;
              box-shadow:none;
      color:rgba(167, 182, 194, 0.6); }
      .bp3-dark .bp3-slider-handle:disabled.bp3-active, .bp3-dark .bp3-slider-handle.bp3-disabled.bp3-active{
        background:rgba(57, 75, 89, 0.7); }
    .bp3-dark .bp3-slider-handle .bp3-button-spinner .bp3-spinner-head{
      background:rgba(16, 22, 26, 0.5);
      stroke:#8a9ba8; }
    .bp3-dark .bp3-slider-handle, .bp3-dark .bp3-slider-handle:hover{
      background-color:#394b59; }
    .bp3-dark .bp3-slider-handle.bp3-active{
      background-color:#293742; }
  .bp3-dark .bp3-disabled .bp3-slider-handle{
    background:#5c7080;
    border-color:#5c7080;
    -webkit-box-shadow:none;
            box-shadow:none; }
  .bp3-slider-handle .bp3-slider-label{
    background:#394b59;
    border-radius:3px;
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 2px 4px rgba(16, 22, 26, 0.2), 0 8px 24px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 2px 4px rgba(16, 22, 26, 0.2), 0 8px 24px rgba(16, 22, 26, 0.2);
    color:#f5f8fa;
    margin-left:8px; }
    .bp3-dark .bp3-slider-handle .bp3-slider-label{
      background:#e1e8ed;
      -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 2px 4px rgba(16, 22, 26, 0.4), 0 8px 24px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 2px 4px rgba(16, 22, 26, 0.4), 0 8px 24px rgba(16, 22, 26, 0.4);
      color:#394b59; }
    .bp3-disabled .bp3-slider-handle .bp3-slider-label{
      -webkit-box-shadow:none;
              box-shadow:none; }
  .bp3-slider-handle.bp3-start, .bp3-slider-handle.bp3-end{
    width:8px; }
  .bp3-slider-handle.bp3-start{
    border-bottom-right-radius:0;
    border-top-right-radius:0; }
  .bp3-slider-handle.bp3-end{
    border-bottom-left-radius:0;
    border-top-left-radius:0;
    margin-left:8px; }
    .bp3-slider-handle.bp3-end .bp3-slider-label{
      margin-left:0; }

.bp3-slider-label{
  -webkit-transform:translate(-50%, 20px);
          transform:translate(-50%, 20px);
  display:inline-block;
  font-size:12px;
  line-height:1;
  padding:2px 5px;
  position:absolute;
  vertical-align:top; }

.bp3-slider.bp3-vertical{
  height:150px;
  min-width:40px;
  width:40px; }
  .bp3-slider.bp3-vertical .bp3-slider-track,
  .bp3-slider.bp3-vertical .bp3-slider-progress{
    bottom:0;
    height:auto;
    left:5px;
    top:0;
    width:6px; }
  .bp3-slider.bp3-vertical .bp3-slider-progress{
    top:auto; }
  .bp3-slider.bp3-vertical .bp3-slider-label{
    -webkit-transform:translate(20px, 50%);
            transform:translate(20px, 50%); }
  .bp3-slider.bp3-vertical .bp3-slider-handle{
    top:auto; }
    .bp3-slider.bp3-vertical .bp3-slider-handle .bp3-slider-label{
      margin-left:0;
      margin-top:-8px; }
    .bp3-slider.bp3-vertical .bp3-slider-handle.bp3-end, .bp3-slider.bp3-vertical .bp3-slider-handle.bp3-start{
      height:8px;
      margin-left:0;
      width:16px; }
    .bp3-slider.bp3-vertical .bp3-slider-handle.bp3-start{
      border-bottom-right-radius:3px;
      border-top-left-radius:0; }
      .bp3-slider.bp3-vertical .bp3-slider-handle.bp3-start .bp3-slider-label{
        -webkit-transform:translate(20px);
                transform:translate(20px); }
    .bp3-slider.bp3-vertical .bp3-slider-handle.bp3-end{
      border-bottom-left-radius:0;
      border-bottom-right-radius:0;
      border-top-left-radius:3px;
      margin-bottom:8px; }

@-webkit-keyframes pt-spinner-animation{
  from{
    -webkit-transform:rotate(0deg);
            transform:rotate(0deg); }
  to{
    -webkit-transform:rotate(360deg);
            transform:rotate(360deg); } }

@keyframes pt-spinner-animation{
  from{
    -webkit-transform:rotate(0deg);
            transform:rotate(0deg); }
  to{
    -webkit-transform:rotate(360deg);
            transform:rotate(360deg); } }

.bp3-spinner{
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center;
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-pack:center;
      -ms-flex-pack:center;
          justify-content:center;
  overflow:visible;
  vertical-align:middle; }
  .bp3-spinner svg{
    display:block; }
  .bp3-spinner path{
    fill-opacity:0; }
  .bp3-spinner .bp3-spinner-head{
    stroke:rgba(92, 112, 128, 0.8);
    stroke-linecap:round;
    -webkit-transform-origin:center;
            transform-origin:center;
    -webkit-transition:stroke-dashoffset 200ms cubic-bezier(0.4, 1, 0.75, 0.9);
    transition:stroke-dashoffset 200ms cubic-bezier(0.4, 1, 0.75, 0.9); }
  .bp3-spinner .bp3-spinner-track{
    stroke:rgba(92, 112, 128, 0.2); }

.bp3-spinner-animation{
  -webkit-animation:pt-spinner-animation 500ms linear infinite;
          animation:pt-spinner-animation 500ms linear infinite; }
  .bp3-no-spin > .bp3-spinner-animation{
    -webkit-animation:none;
            animation:none; }

.bp3-dark .bp3-spinner .bp3-spinner-head{
  stroke:#8a9ba8; }

.bp3-dark .bp3-spinner .bp3-spinner-track{
  stroke:rgba(16, 22, 26, 0.5); }

.bp3-spinner.bp3-intent-primary .bp3-spinner-head{
  stroke:#137cbd; }

.bp3-spinner.bp3-intent-success .bp3-spinner-head{
  stroke:#0f9960; }

.bp3-spinner.bp3-intent-warning .bp3-spinner-head{
  stroke:#d9822b; }

.bp3-spinner.bp3-intent-danger .bp3-spinner-head{
  stroke:#db3737; }
.bp3-tabs.bp3-vertical{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex; }
  .bp3-tabs.bp3-vertical > .bp3-tab-list{
    -webkit-box-align:start;
        -ms-flex-align:start;
            align-items:flex-start;
    -webkit-box-orient:vertical;
    -webkit-box-direction:normal;
        -ms-flex-direction:column;
            flex-direction:column; }
    .bp3-tabs.bp3-vertical > .bp3-tab-list .bp3-tab{
      border-radius:3px;
      padding:0 10px;
      width:100%; }
      .bp3-tabs.bp3-vertical > .bp3-tab-list .bp3-tab[aria-selected="true"]{
        background-color:rgba(19, 124, 189, 0.2);
        -webkit-box-shadow:none;
                box-shadow:none; }
    .bp3-tabs.bp3-vertical > .bp3-tab-list .bp3-tab-indicator-wrapper .bp3-tab-indicator{
      background-color:rgba(19, 124, 189, 0.2);
      border-radius:3px;
      bottom:0;
      height:auto;
      left:0;
      right:0;
      top:0; }
  .bp3-tabs.bp3-vertical > .bp3-tab-panel{
    margin-top:0;
    padding-left:20px; }

.bp3-tab-list{
  -webkit-box-align:end;
      -ms-flex-align:end;
          align-items:flex-end;
  border:none;
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-flex:0;
      -ms-flex:0 0 auto;
          flex:0 0 auto;
  list-style:none;
  margin:0;
  padding:0;
  position:relative; }
  .bp3-tab-list > *:not(:last-child){
    margin-right:20px; }

.bp3-tab{
  overflow:hidden;
  text-overflow:ellipsis;
  white-space:nowrap;
  word-wrap:normal;
  color:#182026;
  cursor:pointer;
  -webkit-box-flex:0;
      -ms-flex:0 0 auto;
          flex:0 0 auto;
  font-size:14px;
  line-height:30px;
  max-width:100%;
  position:relative;
  vertical-align:top; }
  .bp3-tab a{
    color:inherit;
    display:block;
    text-decoration:none; }
  .bp3-tab-indicator-wrapper ~ .bp3-tab{
    background-color:transparent !important;
    -webkit-box-shadow:none !important;
            box-shadow:none !important; }
  .bp3-tab[aria-disabled="true"]{
    color:rgba(92, 112, 128, 0.6);
    cursor:not-allowed; }
  .bp3-tab[aria-selected="true"]{
    border-radius:0;
    -webkit-box-shadow:inset 0 -3px 0 #106ba3;
            box-shadow:inset 0 -3px 0 #106ba3; }
  .bp3-tab[aria-selected="true"], .bp3-tab:not([aria-disabled="true"]):hover{
    color:#106ba3; }
  .bp3-tab:focus{
    -moz-outline-radius:0; }
  .bp3-large > .bp3-tab{
    font-size:16px;
    line-height:40px; }

.bp3-tab-panel{
  margin-top:20px; }
  .bp3-tab-panel[aria-hidden="true"]{
    display:none; }

.bp3-tab-indicator-wrapper{
  left:0;
  pointer-events:none;
  position:absolute;
  top:0;
  -webkit-transform:translateX(0), translateY(0);
          transform:translateX(0), translateY(0);
  -webkit-transition:height, width, -webkit-transform;
  transition:height, width, -webkit-transform;
  transition:height, transform, width;
  transition:height, transform, width, -webkit-transform;
  -webkit-transition-duration:200ms;
          transition-duration:200ms;
  -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
          transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9); }
  .bp3-tab-indicator-wrapper .bp3-tab-indicator{
    background-color:#106ba3;
    bottom:0;
    height:3px;
    left:0;
    position:absolute;
    right:0; }
  .bp3-tab-indicator-wrapper.bp3-no-animation{
    -webkit-transition:none;
    transition:none; }

.bp3-dark .bp3-tab{
  color:#f5f8fa; }
  .bp3-dark .bp3-tab[aria-disabled="true"]{
    color:rgba(167, 182, 194, 0.6); }
  .bp3-dark .bp3-tab[aria-selected="true"]{
    -webkit-box-shadow:inset 0 -3px 0 #48aff0;
            box-shadow:inset 0 -3px 0 #48aff0; }
  .bp3-dark .bp3-tab[aria-selected="true"], .bp3-dark .bp3-tab:not([aria-disabled="true"]):hover{
    color:#48aff0; }

.bp3-dark .bp3-tab-indicator{
  background-color:#48aff0; }

.bp3-flex-expander{
  -webkit-box-flex:1;
      -ms-flex:1 1;
          flex:1 1; }
.bp3-tag{
  display:-webkit-inline-box;
  display:-ms-inline-flexbox;
  display:inline-flex;
  -webkit-box-orient:horizontal;
  -webkit-box-direction:normal;
      -ms-flex-direction:row;
          flex-direction:row;
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center;
  background-color:#5c7080;
  border:none;
  border-radius:3px;
  -webkit-box-shadow:none;
          box-shadow:none;
  color:#f5f8fa;
  font-size:12px;
  line-height:16px;
  max-width:100%;
  min-height:20px;
  min-width:20px;
  padding:2px 6px;
  position:relative; }
  .bp3-tag.bp3-interactive{
    cursor:pointer; }
    .bp3-tag.bp3-interactive:hover{
      background-color:rgba(92, 112, 128, 0.85); }
    .bp3-tag.bp3-interactive.bp3-active, .bp3-tag.bp3-interactive:active{
      background-color:rgba(92, 112, 128, 0.7); }
  .bp3-tag > *{
    -webkit-box-flex:0;
        -ms-flex-positive:0;
            flex-grow:0;
    -ms-flex-negative:0;
        flex-shrink:0; }
  .bp3-tag > .bp3-fill{
    -webkit-box-flex:1;
        -ms-flex-positive:1;
            flex-grow:1;
    -ms-flex-negative:1;
        flex-shrink:1; }
  .bp3-tag::before,
  .bp3-tag > *{
    margin-right:4px; }
  .bp3-tag:empty::before,
  .bp3-tag > :last-child{
    margin-right:0; }
  .bp3-tag:focus{
    outline:rgba(19, 124, 189, 0.6) auto 2px;
    outline-offset:0;
    -moz-outline-radius:6px; }
  .bp3-tag.bp3-round{
    border-radius:30px;
    padding-left:8px;
    padding-right:8px; }
  .bp3-dark .bp3-tag{
    background-color:#bfccd6;
    color:#182026; }
    .bp3-dark .bp3-tag.bp3-interactive{
      cursor:pointer; }
      .bp3-dark .bp3-tag.bp3-interactive:hover{
        background-color:rgba(191, 204, 214, 0.85); }
      .bp3-dark .bp3-tag.bp3-interactive.bp3-active, .bp3-dark .bp3-tag.bp3-interactive:active{
        background-color:rgba(191, 204, 214, 0.7); }
    .bp3-dark .bp3-tag > .bp3-icon, .bp3-dark .bp3-tag .bp3-icon-standard, .bp3-dark .bp3-tag .bp3-icon-large{
      fill:currentColor; }
  .bp3-tag > .bp3-icon, .bp3-tag .bp3-icon-standard, .bp3-tag .bp3-icon-large{
    fill:#ffffff; }
  .bp3-tag.bp3-large,
  .bp3-large .bp3-tag{
    font-size:14px;
    line-height:20px;
    min-height:30px;
    min-width:30px;
    padding:5px 10px; }
    .bp3-tag.bp3-large::before,
    .bp3-tag.bp3-large > *,
    .bp3-large .bp3-tag::before,
    .bp3-large .bp3-tag > *{
      margin-right:7px; }
    .bp3-tag.bp3-large:empty::before,
    .bp3-tag.bp3-large > :last-child,
    .bp3-large .bp3-tag:empty::before,
    .bp3-large .bp3-tag > :last-child{
      margin-right:0; }
    .bp3-tag.bp3-large.bp3-round,
    .bp3-large .bp3-tag.bp3-round{
      padding-left:12px;
      padding-right:12px; }
  .bp3-tag.bp3-intent-primary{
    background:#137cbd;
    color:#ffffff; }
    .bp3-tag.bp3-intent-primary.bp3-interactive{
      cursor:pointer; }
      .bp3-tag.bp3-intent-primary.bp3-interactive:hover{
        background-color:rgba(19, 124, 189, 0.85); }
      .bp3-tag.bp3-intent-primary.bp3-interactive.bp3-active, .bp3-tag.bp3-intent-primary.bp3-interactive:active{
        background-color:rgba(19, 124, 189, 0.7); }
  .bp3-tag.bp3-intent-success{
    background:#0f9960;
    color:#ffffff; }
    .bp3-tag.bp3-intent-success.bp3-interactive{
      cursor:pointer; }
      .bp3-tag.bp3-intent-success.bp3-interactive:hover{
        background-color:rgba(15, 153, 96, 0.85); }
      .bp3-tag.bp3-intent-success.bp3-interactive.bp3-active, .bp3-tag.bp3-intent-success.bp3-interactive:active{
        background-color:rgba(15, 153, 96, 0.7); }
  .bp3-tag.bp3-intent-warning{
    background:#d9822b;
    color:#ffffff; }
    .bp3-tag.bp3-intent-warning.bp3-interactive{
      cursor:pointer; }
      .bp3-tag.bp3-intent-warning.bp3-interactive:hover{
        background-color:rgba(217, 130, 43, 0.85); }
      .bp3-tag.bp3-intent-warning.bp3-interactive.bp3-active, .bp3-tag.bp3-intent-warning.bp3-interactive:active{
        background-color:rgba(217, 130, 43, 0.7); }
  .bp3-tag.bp3-intent-danger{
    background:#db3737;
    color:#ffffff; }
    .bp3-tag.bp3-intent-danger.bp3-interactive{
      cursor:pointer; }
      .bp3-tag.bp3-intent-danger.bp3-interactive:hover{
        background-color:rgba(219, 55, 55, 0.85); }
      .bp3-tag.bp3-intent-danger.bp3-interactive.bp3-active, .bp3-tag.bp3-intent-danger.bp3-interactive:active{
        background-color:rgba(219, 55, 55, 0.7); }
  .bp3-tag.bp3-fill{
    display:-webkit-box;
    display:-ms-flexbox;
    display:flex;
    width:100%; }
  .bp3-tag.bp3-minimal > .bp3-icon, .bp3-tag.bp3-minimal .bp3-icon-standard, .bp3-tag.bp3-minimal .bp3-icon-large{
    fill:#5c7080; }
  .bp3-tag.bp3-minimal:not([class*="bp3-intent-"]){
    background-color:rgba(138, 155, 168, 0.2);
    color:#182026; }
    .bp3-tag.bp3-minimal:not([class*="bp3-intent-"]).bp3-interactive{
      cursor:pointer; }
      .bp3-tag.bp3-minimal:not([class*="bp3-intent-"]).bp3-interactive:hover{
        background-color:rgba(92, 112, 128, 0.3); }
      .bp3-tag.bp3-minimal:not([class*="bp3-intent-"]).bp3-interactive.bp3-active, .bp3-tag.bp3-minimal:not([class*="bp3-intent-"]).bp3-interactive:active{
        background-color:rgba(92, 112, 128, 0.4); }
    .bp3-dark .bp3-tag.bp3-minimal:not([class*="bp3-intent-"]){
      color:#f5f8fa; }
      .bp3-dark .bp3-tag.bp3-minimal:not([class*="bp3-intent-"]).bp3-interactive{
        cursor:pointer; }
        .bp3-dark .bp3-tag.bp3-minimal:not([class*="bp3-intent-"]).bp3-interactive:hover{
          background-color:rgba(191, 204, 214, 0.3); }
        .bp3-dark .bp3-tag.bp3-minimal:not([class*="bp3-intent-"]).bp3-interactive.bp3-active, .bp3-dark .bp3-tag.bp3-minimal:not([class*="bp3-intent-"]).bp3-interactive:active{
          background-color:rgba(191, 204, 214, 0.4); }
      .bp3-dark .bp3-tag.bp3-minimal:not([class*="bp3-intent-"]) > .bp3-icon, .bp3-dark .bp3-tag.bp3-minimal:not([class*="bp3-intent-"]) .bp3-icon-standard, .bp3-dark .bp3-tag.bp3-minimal:not([class*="bp3-intent-"]) .bp3-icon-large{
        fill:#a7b6c2; }
  .bp3-tag.bp3-minimal.bp3-intent-primary{
    background-color:rgba(19, 124, 189, 0.15);
    color:#106ba3; }
    .bp3-tag.bp3-minimal.bp3-intent-primary.bp3-interactive{
      cursor:pointer; }
      .bp3-tag.bp3-minimal.bp3-intent-primary.bp3-interactive:hover{
        background-color:rgba(19, 124, 189, 0.25); }
      .bp3-tag.bp3-minimal.bp3-intent-primary.bp3-interactive.bp3-active, .bp3-tag.bp3-minimal.bp3-intent-primary.bp3-interactive:active{
        background-color:rgba(19, 124, 189, 0.35); }
    .bp3-tag.bp3-minimal.bp3-intent-primary > .bp3-icon, .bp3-tag.bp3-minimal.bp3-intent-primary .bp3-icon-standard, .bp3-tag.bp3-minimal.bp3-intent-primary .bp3-icon-large{
      fill:#137cbd; }
    .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-primary{
      background-color:rgba(19, 124, 189, 0.25);
      color:#48aff0; }
      .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-primary.bp3-interactive{
        cursor:pointer; }
        .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-primary.bp3-interactive:hover{
          background-color:rgba(19, 124, 189, 0.35); }
        .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-primary.bp3-interactive.bp3-active, .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-primary.bp3-interactive:active{
          background-color:rgba(19, 124, 189, 0.45); }
  .bp3-tag.bp3-minimal.bp3-intent-success{
    background-color:rgba(15, 153, 96, 0.15);
    color:#0d8050; }
    .bp3-tag.bp3-minimal.bp3-intent-success.bp3-interactive{
      cursor:pointer; }
      .bp3-tag.bp3-minimal.bp3-intent-success.bp3-interactive:hover{
        background-color:rgba(15, 153, 96, 0.25); }
      .bp3-tag.bp3-minimal.bp3-intent-success.bp3-interactive.bp3-active, .bp3-tag.bp3-minimal.bp3-intent-success.bp3-interactive:active{
        background-color:rgba(15, 153, 96, 0.35); }
    .bp3-tag.bp3-minimal.bp3-intent-success > .bp3-icon, .bp3-tag.bp3-minimal.bp3-intent-success .bp3-icon-standard, .bp3-tag.bp3-minimal.bp3-intent-success .bp3-icon-large{
      fill:#0f9960; }
    .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-success{
      background-color:rgba(15, 153, 96, 0.25);
      color:#3dcc91; }
      .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-success.bp3-interactive{
        cursor:pointer; }
        .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-success.bp3-interactive:hover{
          background-color:rgba(15, 153, 96, 0.35); }
        .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-success.bp3-interactive.bp3-active, .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-success.bp3-interactive:active{
          background-color:rgba(15, 153, 96, 0.45); }
  .bp3-tag.bp3-minimal.bp3-intent-warning{
    background-color:rgba(217, 130, 43, 0.15);
    color:#bf7326; }
    .bp3-tag.bp3-minimal.bp3-intent-warning.bp3-interactive{
      cursor:pointer; }
      .bp3-tag.bp3-minimal.bp3-intent-warning.bp3-interactive:hover{
        background-color:rgba(217, 130, 43, 0.25); }
      .bp3-tag.bp3-minimal.bp3-intent-warning.bp3-interactive.bp3-active, .bp3-tag.bp3-minimal.bp3-intent-warning.bp3-interactive:active{
        background-color:rgba(217, 130, 43, 0.35); }
    .bp3-tag.bp3-minimal.bp3-intent-warning > .bp3-icon, .bp3-tag.bp3-minimal.bp3-intent-warning .bp3-icon-standard, .bp3-tag.bp3-minimal.bp3-intent-warning .bp3-icon-large{
      fill:#d9822b; }
    .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-warning{
      background-color:rgba(217, 130, 43, 0.25);
      color:#ffb366; }
      .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-warning.bp3-interactive{
        cursor:pointer; }
        .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-warning.bp3-interactive:hover{
          background-color:rgba(217, 130, 43, 0.35); }
        .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-warning.bp3-interactive.bp3-active, .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-warning.bp3-interactive:active{
          background-color:rgba(217, 130, 43, 0.45); }
  .bp3-tag.bp3-minimal.bp3-intent-danger{
    background-color:rgba(219, 55, 55, 0.15);
    color:#c23030; }
    .bp3-tag.bp3-minimal.bp3-intent-danger.bp3-interactive{
      cursor:pointer; }
      .bp3-tag.bp3-minimal.bp3-intent-danger.bp3-interactive:hover{
        background-color:rgba(219, 55, 55, 0.25); }
      .bp3-tag.bp3-minimal.bp3-intent-danger.bp3-interactive.bp3-active, .bp3-tag.bp3-minimal.bp3-intent-danger.bp3-interactive:active{
        background-color:rgba(219, 55, 55, 0.35); }
    .bp3-tag.bp3-minimal.bp3-intent-danger > .bp3-icon, .bp3-tag.bp3-minimal.bp3-intent-danger .bp3-icon-standard, .bp3-tag.bp3-minimal.bp3-intent-danger .bp3-icon-large{
      fill:#db3737; }
    .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-danger{
      background-color:rgba(219, 55, 55, 0.25);
      color:#ff7373; }
      .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-danger.bp3-interactive{
        cursor:pointer; }
        .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-danger.bp3-interactive:hover{
          background-color:rgba(219, 55, 55, 0.35); }
        .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-danger.bp3-interactive.bp3-active, .bp3-dark .bp3-tag.bp3-minimal.bp3-intent-danger.bp3-interactive:active{
          background-color:rgba(219, 55, 55, 0.45); }

.bp3-tag-remove{
  background:none;
  border:none;
  color:inherit;
  cursor:pointer;
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  margin-bottom:-2px;
  margin-right:-6px !important;
  margin-top:-2px;
  opacity:0.5;
  padding:2px;
  padding-left:0; }
  .bp3-tag-remove:hover{
    background:none;
    opacity:0.8;
    text-decoration:none; }
  .bp3-tag-remove:active{
    opacity:1; }
  .bp3-tag-remove:empty::before{
    font-family:"Icons16", sans-serif;
    font-size:16px;
    font-style:normal;
    font-weight:400;
    line-height:1;
    -moz-osx-font-smoothing:grayscale;
    -webkit-font-smoothing:antialiased;
    content:""; }
  .bp3-large .bp3-tag-remove{
    margin-right:-10px !important;
    padding:0 5px 0 0; }
    .bp3-large .bp3-tag-remove:empty::before{
      font-family:"Icons20", sans-serif;
      font-size:20px;
      font-style:normal;
      font-weight:400;
      line-height:1; }
.bp3-tag-input{
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  -webkit-box-orient:horizontal;
  -webkit-box-direction:normal;
      -ms-flex-direction:row;
          flex-direction:row;
  -webkit-box-align:start;
      -ms-flex-align:start;
          align-items:flex-start;
  cursor:text;
  height:auto;
  line-height:inherit;
  min-height:30px;
  padding-left:5px;
  padding-right:0; }
  .bp3-tag-input > *{
    -webkit-box-flex:0;
        -ms-flex-positive:0;
            flex-grow:0;
    -ms-flex-negative:0;
        flex-shrink:0; }
  .bp3-tag-input > .bp3-tag-input-values{
    -webkit-box-flex:1;
        -ms-flex-positive:1;
            flex-grow:1;
    -ms-flex-negative:1;
        flex-shrink:1; }
  .bp3-tag-input .bp3-tag-input-icon{
    color:#5c7080;
    margin-left:2px;
    margin-right:7px;
    margin-top:7px; }
  .bp3-tag-input .bp3-tag-input-values{
    display:-webkit-box;
    display:-ms-flexbox;
    display:flex;
    -webkit-box-orient:horizontal;
    -webkit-box-direction:normal;
        -ms-flex-direction:row;
            flex-direction:row;
    -webkit-box-align:center;
        -ms-flex-align:center;
            align-items:center;
    -ms-flex-item-align:stretch;
        align-self:stretch;
    -ms-flex-wrap:wrap;
        flex-wrap:wrap;
    margin-right:7px;
    margin-top:5px;
    min-width:0; }
    .bp3-tag-input .bp3-tag-input-values > *{
      -webkit-box-flex:0;
          -ms-flex-positive:0;
              flex-grow:0;
      -ms-flex-negative:0;
          flex-shrink:0; }
    .bp3-tag-input .bp3-tag-input-values > .bp3-fill{
      -webkit-box-flex:1;
          -ms-flex-positive:1;
              flex-grow:1;
      -ms-flex-negative:1;
          flex-shrink:1; }
    .bp3-tag-input .bp3-tag-input-values::before,
    .bp3-tag-input .bp3-tag-input-values > *{
      margin-right:5px; }
    .bp3-tag-input .bp3-tag-input-values:empty::before,
    .bp3-tag-input .bp3-tag-input-values > :last-child{
      margin-right:0; }
    .bp3-tag-input .bp3-tag-input-values:first-child .bp3-input-ghost:first-child{
      padding-left:5px; }
    .bp3-tag-input .bp3-tag-input-values > *{
      margin-bottom:5px; }
  .bp3-tag-input .bp3-tag{
    overflow-wrap:break-word; }
    .bp3-tag-input .bp3-tag.bp3-active{
      outline:rgba(19, 124, 189, 0.6) auto 2px;
      outline-offset:0;
      -moz-outline-radius:6px; }
  .bp3-tag-input .bp3-input-ghost{
    -webkit-box-flex:1;
        -ms-flex:1 1 auto;
            flex:1 1 auto;
    line-height:20px;
    width:80px; }
    .bp3-tag-input .bp3-input-ghost:disabled, .bp3-tag-input .bp3-input-ghost.bp3-disabled{
      cursor:not-allowed; }
  .bp3-tag-input .bp3-button,
  .bp3-tag-input .bp3-spinner{
    margin:3px;
    margin-left:0; }
  .bp3-tag-input .bp3-button{
    min-height:24px;
    min-width:24px;
    padding:0 7px; }
  .bp3-tag-input.bp3-large{
    height:auto;
    min-height:40px; }
    .bp3-tag-input.bp3-large::before,
    .bp3-tag-input.bp3-large > *{
      margin-right:10px; }
    .bp3-tag-input.bp3-large:empty::before,
    .bp3-tag-input.bp3-large > :last-child{
      margin-right:0; }
    .bp3-tag-input.bp3-large .bp3-tag-input-icon{
      margin-left:5px;
      margin-top:10px; }
    .bp3-tag-input.bp3-large .bp3-input-ghost{
      line-height:30px; }
    .bp3-tag-input.bp3-large .bp3-button{
      min-height:30px;
      min-width:30px;
      padding:5px 10px;
      margin:5px;
      margin-left:0; }
    .bp3-tag-input.bp3-large .bp3-spinner{
      margin:8px;
      margin-left:0; }
  .bp3-tag-input.bp3-active{
    background-color:#ffffff;
    -webkit-box-shadow:0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
            box-shadow:0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-tag-input.bp3-active.bp3-intent-primary{
      -webkit-box-shadow:0 0 0 1px #106ba3, 0 0 0 3px rgba(16, 107, 163, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px #106ba3, 0 0 0 3px rgba(16, 107, 163, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-tag-input.bp3-active.bp3-intent-success{
      -webkit-box-shadow:0 0 0 1px #0d8050, 0 0 0 3px rgba(13, 128, 80, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px #0d8050, 0 0 0 3px rgba(13, 128, 80, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-tag-input.bp3-active.bp3-intent-warning{
      -webkit-box-shadow:0 0 0 1px #bf7326, 0 0 0 3px rgba(191, 115, 38, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px #bf7326, 0 0 0 3px rgba(191, 115, 38, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
    .bp3-tag-input.bp3-active.bp3-intent-danger{
      -webkit-box-shadow:0 0 0 1px #c23030, 0 0 0 3px rgba(194, 48, 48, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2);
              box-shadow:0 0 0 1px #c23030, 0 0 0 3px rgba(194, 48, 48, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.2); }
  .bp3-dark .bp3-tag-input .bp3-tag-input-icon, .bp3-tag-input.bp3-dark .bp3-tag-input-icon{
    color:#a7b6c2; }
  .bp3-dark .bp3-tag-input .bp3-input-ghost, .bp3-tag-input.bp3-dark .bp3-input-ghost{
    color:#f5f8fa; }
    .bp3-dark .bp3-tag-input .bp3-input-ghost::-webkit-input-placeholder, .bp3-tag-input.bp3-dark .bp3-input-ghost::-webkit-input-placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-tag-input .bp3-input-ghost::-moz-placeholder, .bp3-tag-input.bp3-dark .bp3-input-ghost::-moz-placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-tag-input .bp3-input-ghost:-ms-input-placeholder, .bp3-tag-input.bp3-dark .bp3-input-ghost:-ms-input-placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-tag-input .bp3-input-ghost::-ms-input-placeholder, .bp3-tag-input.bp3-dark .bp3-input-ghost::-ms-input-placeholder{
      color:rgba(167, 182, 194, 0.6); }
    .bp3-dark .bp3-tag-input .bp3-input-ghost::placeholder, .bp3-tag-input.bp3-dark .bp3-input-ghost::placeholder{
      color:rgba(167, 182, 194, 0.6); }
  .bp3-dark .bp3-tag-input.bp3-active, .bp3-tag-input.bp3-dark.bp3-active{
    background-color:rgba(16, 22, 26, 0.3);
    -webkit-box-shadow:0 0 0 1px #137cbd, 0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px #137cbd, 0 0 0 1px #137cbd, 0 0 0 3px rgba(19, 124, 189, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
    .bp3-dark .bp3-tag-input.bp3-active.bp3-intent-primary, .bp3-tag-input.bp3-dark.bp3-active.bp3-intent-primary{
      -webkit-box-shadow:0 0 0 1px #106ba3, 0 0 0 3px rgba(16, 107, 163, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 1px #106ba3, 0 0 0 3px rgba(16, 107, 163, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
    .bp3-dark .bp3-tag-input.bp3-active.bp3-intent-success, .bp3-tag-input.bp3-dark.bp3-active.bp3-intent-success{
      -webkit-box-shadow:0 0 0 1px #0d8050, 0 0 0 3px rgba(13, 128, 80, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 1px #0d8050, 0 0 0 3px rgba(13, 128, 80, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
    .bp3-dark .bp3-tag-input.bp3-active.bp3-intent-warning, .bp3-tag-input.bp3-dark.bp3-active.bp3-intent-warning{
      -webkit-box-shadow:0 0 0 1px #bf7326, 0 0 0 3px rgba(191, 115, 38, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 1px #bf7326, 0 0 0 3px rgba(191, 115, 38, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }
    .bp3-dark .bp3-tag-input.bp3-active.bp3-intent-danger, .bp3-tag-input.bp3-dark.bp3-active.bp3-intent-danger{
      -webkit-box-shadow:0 0 0 1px #c23030, 0 0 0 3px rgba(194, 48, 48, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4);
              box-shadow:0 0 0 1px #c23030, 0 0 0 3px rgba(194, 48, 48, 0.3), inset 0 0 0 1px rgba(16, 22, 26, 0.3), inset 0 1px 1px rgba(16, 22, 26, 0.4); }

.bp3-input-ghost{
  background:none;
  border:none;
  -webkit-box-shadow:none;
          box-shadow:none;
  padding:0; }
  .bp3-input-ghost::-webkit-input-placeholder{
    color:rgba(92, 112, 128, 0.6);
    opacity:1; }
  .bp3-input-ghost::-moz-placeholder{
    color:rgba(92, 112, 128, 0.6);
    opacity:1; }
  .bp3-input-ghost:-ms-input-placeholder{
    color:rgba(92, 112, 128, 0.6);
    opacity:1; }
  .bp3-input-ghost::-ms-input-placeholder{
    color:rgba(92, 112, 128, 0.6);
    opacity:1; }
  .bp3-input-ghost::placeholder{
    color:rgba(92, 112, 128, 0.6);
    opacity:1; }
  .bp3-input-ghost:focus{
    outline:none !important; }
.bp3-toast{
  -webkit-box-align:start;
      -ms-flex-align:start;
          align-items:flex-start;
  background-color:#ffffff;
  border-radius:3px;
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 2px 4px rgba(16, 22, 26, 0.2), 0 8px 24px rgba(16, 22, 26, 0.2);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 2px 4px rgba(16, 22, 26, 0.2), 0 8px 24px rgba(16, 22, 26, 0.2);
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  margin:20px 0 0;
  max-width:500px;
  min-width:300px;
  pointer-events:all;
  position:relative !important; }
  .bp3-toast.bp3-toast-enter, .bp3-toast.bp3-toast-appear{
    -webkit-transform:translateY(-40px);
            transform:translateY(-40px); }
  .bp3-toast.bp3-toast-enter-active, .bp3-toast.bp3-toast-appear-active{
    -webkit-transform:translateY(0);
            transform:translateY(0);
    -webkit-transition-delay:0;
            transition-delay:0;
    -webkit-transition-duration:300ms;
            transition-duration:300ms;
    -webkit-transition-property:-webkit-transform;
    transition-property:-webkit-transform;
    transition-property:transform;
    transition-property:transform, -webkit-transform;
    -webkit-transition-timing-function:cubic-bezier(0.54, 1.12, 0.38, 1.11);
            transition-timing-function:cubic-bezier(0.54, 1.12, 0.38, 1.11); }
  .bp3-toast.bp3-toast-enter ~ .bp3-toast, .bp3-toast.bp3-toast-appear ~ .bp3-toast{
    -webkit-transform:translateY(-40px);
            transform:translateY(-40px); }
  .bp3-toast.bp3-toast-enter-active ~ .bp3-toast, .bp3-toast.bp3-toast-appear-active ~ .bp3-toast{
    -webkit-transform:translateY(0);
            transform:translateY(0);
    -webkit-transition-delay:0;
            transition-delay:0;
    -webkit-transition-duration:300ms;
            transition-duration:300ms;
    -webkit-transition-property:-webkit-transform;
    transition-property:-webkit-transform;
    transition-property:transform;
    transition-property:transform, -webkit-transform;
    -webkit-transition-timing-function:cubic-bezier(0.54, 1.12, 0.38, 1.11);
            transition-timing-function:cubic-bezier(0.54, 1.12, 0.38, 1.11); }
  .bp3-toast.bp3-toast-exit{
    opacity:1;
    -webkit-filter:blur(0);
            filter:blur(0); }
  .bp3-toast.bp3-toast-exit-active{
    opacity:0;
    -webkit-filter:blur(10px);
            filter:blur(10px);
    -webkit-transition-delay:0;
            transition-delay:0;
    -webkit-transition-duration:300ms;
            transition-duration:300ms;
    -webkit-transition-property:opacity, -webkit-filter;
    transition-property:opacity, -webkit-filter;
    transition-property:opacity, filter;
    transition-property:opacity, filter, -webkit-filter;
    -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
            transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9); }
  .bp3-toast.bp3-toast-exit ~ .bp3-toast{
    -webkit-transform:translateY(0);
            transform:translateY(0); }
  .bp3-toast.bp3-toast-exit-active ~ .bp3-toast{
    -webkit-transform:translateY(-40px);
            transform:translateY(-40px);
    -webkit-transition-delay:50ms;
            transition-delay:50ms;
    -webkit-transition-duration:100ms;
            transition-duration:100ms;
    -webkit-transition-property:-webkit-transform;
    transition-property:-webkit-transform;
    transition-property:transform;
    transition-property:transform, -webkit-transform;
    -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
            transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9); }
  .bp3-toast .bp3-button-group{
    -webkit-box-flex:0;
        -ms-flex:0 0 auto;
            flex:0 0 auto;
    padding:5px;
    padding-left:0; }
  .bp3-toast > .bp3-icon{
    color:#5c7080;
    margin:12px;
    margin-right:0; }
  .bp3-toast.bp3-dark,
  .bp3-dark .bp3-toast{
    background-color:#394b59;
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 2px 4px rgba(16, 22, 26, 0.4), 0 8px 24px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 2px 4px rgba(16, 22, 26, 0.4), 0 8px 24px rgba(16, 22, 26, 0.4); }
    .bp3-toast.bp3-dark > .bp3-icon,
    .bp3-dark .bp3-toast > .bp3-icon{
      color:#a7b6c2; }
  .bp3-toast[class*="bp3-intent-"] a{
    color:rgba(255, 255, 255, 0.7); }
    .bp3-toast[class*="bp3-intent-"] a:hover{
      color:#ffffff; }
  .bp3-toast[class*="bp3-intent-"] > .bp3-icon{
    color:#ffffff; }
  .bp3-toast[class*="bp3-intent-"] .bp3-button, .bp3-toast[class*="bp3-intent-"] .bp3-button::before,
  .bp3-toast[class*="bp3-intent-"] .bp3-button .bp3-icon, .bp3-toast[class*="bp3-intent-"] .bp3-button:active{
    color:rgba(255, 255, 255, 0.7) !important; }
  .bp3-toast[class*="bp3-intent-"] .bp3-button:focus{
    outline-color:rgba(255, 255, 255, 0.5); }
  .bp3-toast[class*="bp3-intent-"] .bp3-button:hover{
    background-color:rgba(255, 255, 255, 0.15) !important;
    color:#ffffff !important; }
  .bp3-toast[class*="bp3-intent-"] .bp3-button:active{
    background-color:rgba(255, 255, 255, 0.3) !important;
    color:#ffffff !important; }
  .bp3-toast[class*="bp3-intent-"] .bp3-button::after{
    background:rgba(255, 255, 255, 0.3) !important; }
  .bp3-toast.bp3-intent-primary{
    background-color:#137cbd;
    color:#ffffff; }
  .bp3-toast.bp3-intent-success{
    background-color:#0f9960;
    color:#ffffff; }
  .bp3-toast.bp3-intent-warning{
    background-color:#d9822b;
    color:#ffffff; }
  .bp3-toast.bp3-intent-danger{
    background-color:#db3737;
    color:#ffffff; }

.bp3-toast-message{
  -webkit-box-flex:1;
      -ms-flex:1 1 auto;
          flex:1 1 auto;
  padding:11px;
  word-break:break-word; }

.bp3-toast-container{
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center;
  display:-webkit-box !important;
  display:-ms-flexbox !important;
  display:flex !important;
  -webkit-box-orient:vertical;
  -webkit-box-direction:normal;
      -ms-flex-direction:column;
          flex-direction:column;
  left:0;
  overflow:hidden;
  padding:0 20px 20px;
  pointer-events:none;
  right:0;
  z-index:40; }
  .bp3-toast-container.bp3-toast-container-in-portal{
    position:fixed; }
  .bp3-toast-container.bp3-toast-container-inline{
    position:absolute; }
  .bp3-toast-container.bp3-toast-container-top{
    top:0; }
  .bp3-toast-container.bp3-toast-container-bottom{
    bottom:0;
    -webkit-box-orient:vertical;
    -webkit-box-direction:reverse;
        -ms-flex-direction:column-reverse;
            flex-direction:column-reverse;
    top:auto; }
  .bp3-toast-container.bp3-toast-container-left{
    -webkit-box-align:start;
        -ms-flex-align:start;
            align-items:flex-start; }
  .bp3-toast-container.bp3-toast-container-right{
    -webkit-box-align:end;
        -ms-flex-align:end;
            align-items:flex-end; }

.bp3-toast-container-bottom .bp3-toast.bp3-toast-enter:not(.bp3-toast-enter-active),
.bp3-toast-container-bottom .bp3-toast.bp3-toast-enter:not(.bp3-toast-enter-active) ~ .bp3-toast, .bp3-toast-container-bottom .bp3-toast.bp3-toast-appear:not(.bp3-toast-appear-active),
.bp3-toast-container-bottom .bp3-toast.bp3-toast-appear:not(.bp3-toast-appear-active) ~ .bp3-toast,
.bp3-toast-container-bottom .bp3-toast.bp3-toast-exit-active ~ .bp3-toast,
.bp3-toast-container-bottom .bp3-toast.bp3-toast-leave-active ~ .bp3-toast{
  -webkit-transform:translateY(60px);
          transform:translateY(60px); }
.bp3-tooltip{
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 2px 4px rgba(16, 22, 26, 0.2), 0 8px 24px rgba(16, 22, 26, 0.2);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 2px 4px rgba(16, 22, 26, 0.2), 0 8px 24px rgba(16, 22, 26, 0.2);
  -webkit-transform:scale(1);
          transform:scale(1); }
  .bp3-tooltip .bp3-popover-arrow{
    height:22px;
    position:absolute;
    width:22px; }
    .bp3-tooltip .bp3-popover-arrow::before{
      height:14px;
      margin:4px;
      width:14px; }
  .bp3-tether-element-attached-bottom.bp3-tether-target-attached-top > .bp3-tooltip{
    margin-bottom:11px;
    margin-top:-11px; }
    .bp3-tether-element-attached-bottom.bp3-tether-target-attached-top > .bp3-tooltip > .bp3-popover-arrow{
      bottom:-8px; }
      .bp3-tether-element-attached-bottom.bp3-tether-target-attached-top > .bp3-tooltip > .bp3-popover-arrow svg{
        -webkit-transform:rotate(-90deg);
                transform:rotate(-90deg); }
  .bp3-tether-element-attached-left.bp3-tether-target-attached-right > .bp3-tooltip{
    margin-left:11px; }
    .bp3-tether-element-attached-left.bp3-tether-target-attached-right > .bp3-tooltip > .bp3-popover-arrow{
      left:-8px; }
      .bp3-tether-element-attached-left.bp3-tether-target-attached-right > .bp3-tooltip > .bp3-popover-arrow svg{
        -webkit-transform:rotate(0);
                transform:rotate(0); }
  .bp3-tether-element-attached-top.bp3-tether-target-attached-bottom > .bp3-tooltip{
    margin-top:11px; }
    .bp3-tether-element-attached-top.bp3-tether-target-attached-bottom > .bp3-tooltip > .bp3-popover-arrow{
      top:-8px; }
      .bp3-tether-element-attached-top.bp3-tether-target-attached-bottom > .bp3-tooltip > .bp3-popover-arrow svg{
        -webkit-transform:rotate(90deg);
                transform:rotate(90deg); }
  .bp3-tether-element-attached-right.bp3-tether-target-attached-left > .bp3-tooltip{
    margin-left:-11px;
    margin-right:11px; }
    .bp3-tether-element-attached-right.bp3-tether-target-attached-left > .bp3-tooltip > .bp3-popover-arrow{
      right:-8px; }
      .bp3-tether-element-attached-right.bp3-tether-target-attached-left > .bp3-tooltip > .bp3-popover-arrow svg{
        -webkit-transform:rotate(180deg);
                transform:rotate(180deg); }
  .bp3-tether-element-attached-middle > .bp3-tooltip > .bp3-popover-arrow{
    top:50%;
    -webkit-transform:translateY(-50%);
            transform:translateY(-50%); }
  .bp3-tether-element-attached-center > .bp3-tooltip > .bp3-popover-arrow{
    right:50%;
    -webkit-transform:translateX(50%);
            transform:translateX(50%); }
  .bp3-tether-element-attached-top.bp3-tether-target-attached-top > .bp3-tooltip > .bp3-popover-arrow{
    top:-0.22183px; }
  .bp3-tether-element-attached-right.bp3-tether-target-attached-right > .bp3-tooltip > .bp3-popover-arrow{
    right:-0.22183px; }
  .bp3-tether-element-attached-left.bp3-tether-target-attached-left > .bp3-tooltip > .bp3-popover-arrow{
    left:-0.22183px; }
  .bp3-tether-element-attached-bottom.bp3-tether-target-attached-bottom > .bp3-tooltip > .bp3-popover-arrow{
    bottom:-0.22183px; }
  .bp3-tether-element-attached-top.bp3-tether-element-attached-left > .bp3-tooltip{
    -webkit-transform-origin:top left;
            transform-origin:top left; }
  .bp3-tether-element-attached-top.bp3-tether-element-attached-center > .bp3-tooltip{
    -webkit-transform-origin:top center;
            transform-origin:top center; }
  .bp3-tether-element-attached-top.bp3-tether-element-attached-right > .bp3-tooltip{
    -webkit-transform-origin:top right;
            transform-origin:top right; }
  .bp3-tether-element-attached-middle.bp3-tether-element-attached-left > .bp3-tooltip{
    -webkit-transform-origin:center left;
            transform-origin:center left; }
  .bp3-tether-element-attached-middle.bp3-tether-element-attached-center > .bp3-tooltip{
    -webkit-transform-origin:center center;
            transform-origin:center center; }
  .bp3-tether-element-attached-middle.bp3-tether-element-attached-right > .bp3-tooltip{
    -webkit-transform-origin:center right;
            transform-origin:center right; }
  .bp3-tether-element-attached-bottom.bp3-tether-element-attached-left > .bp3-tooltip{
    -webkit-transform-origin:bottom left;
            transform-origin:bottom left; }
  .bp3-tether-element-attached-bottom.bp3-tether-element-attached-center > .bp3-tooltip{
    -webkit-transform-origin:bottom center;
            transform-origin:bottom center; }
  .bp3-tether-element-attached-bottom.bp3-tether-element-attached-right > .bp3-tooltip{
    -webkit-transform-origin:bottom right;
            transform-origin:bottom right; }
  .bp3-tooltip .bp3-popover-content{
    background:#394b59;
    color:#f5f8fa; }
  .bp3-tooltip .bp3-popover-arrow::before{
    -webkit-box-shadow:1px 1px 6px rgba(16, 22, 26, 0.2);
            box-shadow:1px 1px 6px rgba(16, 22, 26, 0.2); }
  .bp3-tooltip .bp3-popover-arrow-border{
    fill:#10161a;
    fill-opacity:0.1; }
  .bp3-tooltip .bp3-popover-arrow-fill{
    fill:#394b59; }
  .bp3-popover-enter > .bp3-tooltip, .bp3-popover-appear > .bp3-tooltip{
    -webkit-transform:scale(0.8);
            transform:scale(0.8); }
  .bp3-popover-enter-active > .bp3-tooltip, .bp3-popover-appear-active > .bp3-tooltip{
    -webkit-transform:scale(1);
            transform:scale(1);
    -webkit-transition-delay:0;
            transition-delay:0;
    -webkit-transition-duration:100ms;
            transition-duration:100ms;
    -webkit-transition-property:-webkit-transform;
    transition-property:-webkit-transform;
    transition-property:transform;
    transition-property:transform, -webkit-transform;
    -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
            transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9); }
  .bp3-popover-exit > .bp3-tooltip{
    -webkit-transform:scale(1);
            transform:scale(1); }
  .bp3-popover-exit-active > .bp3-tooltip{
    -webkit-transform:scale(0.8);
            transform:scale(0.8);
    -webkit-transition-delay:0;
            transition-delay:0;
    -webkit-transition-duration:100ms;
            transition-duration:100ms;
    -webkit-transition-property:-webkit-transform;
    transition-property:-webkit-transform;
    transition-property:transform;
    transition-property:transform, -webkit-transform;
    -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
            transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9); }
  .bp3-tooltip .bp3-popover-content{
    padding:10px 12px; }
  .bp3-tooltip.bp3-dark,
  .bp3-dark .bp3-tooltip{
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 2px 4px rgba(16, 22, 26, 0.4), 0 8px 24px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 2px 4px rgba(16, 22, 26, 0.4), 0 8px 24px rgba(16, 22, 26, 0.4); }
    .bp3-tooltip.bp3-dark .bp3-popover-content,
    .bp3-dark .bp3-tooltip .bp3-popover-content{
      background:#e1e8ed;
      color:#394b59; }
    .bp3-tooltip.bp3-dark .bp3-popover-arrow::before,
    .bp3-dark .bp3-tooltip .bp3-popover-arrow::before{
      -webkit-box-shadow:1px 1px 6px rgba(16, 22, 26, 0.4);
              box-shadow:1px 1px 6px rgba(16, 22, 26, 0.4); }
    .bp3-tooltip.bp3-dark .bp3-popover-arrow-border,
    .bp3-dark .bp3-tooltip .bp3-popover-arrow-border{
      fill:#10161a;
      fill-opacity:0.2; }
    .bp3-tooltip.bp3-dark .bp3-popover-arrow-fill,
    .bp3-dark .bp3-tooltip .bp3-popover-arrow-fill{
      fill:#e1e8ed; }
  .bp3-tooltip.bp3-intent-primary .bp3-popover-content{
    background:#137cbd;
    color:#ffffff; }
  .bp3-tooltip.bp3-intent-primary .bp3-popover-arrow-fill{
    fill:#137cbd; }
  .bp3-tooltip.bp3-intent-success .bp3-popover-content{
    background:#0f9960;
    color:#ffffff; }
  .bp3-tooltip.bp3-intent-success .bp3-popover-arrow-fill{
    fill:#0f9960; }
  .bp3-tooltip.bp3-intent-warning .bp3-popover-content{
    background:#d9822b;
    color:#ffffff; }
  .bp3-tooltip.bp3-intent-warning .bp3-popover-arrow-fill{
    fill:#d9822b; }
  .bp3-tooltip.bp3-intent-danger .bp3-popover-content{
    background:#db3737;
    color:#ffffff; }
  .bp3-tooltip.bp3-intent-danger .bp3-popover-arrow-fill{
    fill:#db3737; }

.bp3-tooltip-indicator{
  border-bottom:dotted 1px;
  cursor:help; }
.bp3-tree .bp3-icon, .bp3-tree .bp3-icon-standard, .bp3-tree .bp3-icon-large{
  color:#5c7080; }
  .bp3-tree .bp3-icon.bp3-intent-primary, .bp3-tree .bp3-icon-standard.bp3-intent-primary, .bp3-tree .bp3-icon-large.bp3-intent-primary{
    color:#137cbd; }
  .bp3-tree .bp3-icon.bp3-intent-success, .bp3-tree .bp3-icon-standard.bp3-intent-success, .bp3-tree .bp3-icon-large.bp3-intent-success{
    color:#0f9960; }
  .bp3-tree .bp3-icon.bp3-intent-warning, .bp3-tree .bp3-icon-standard.bp3-intent-warning, .bp3-tree .bp3-icon-large.bp3-intent-warning{
    color:#d9822b; }
  .bp3-tree .bp3-icon.bp3-intent-danger, .bp3-tree .bp3-icon-standard.bp3-intent-danger, .bp3-tree .bp3-icon-large.bp3-intent-danger{
    color:#db3737; }

.bp3-tree-node-list{
  list-style:none;
  margin:0;
  padding-left:0; }

.bp3-tree-root{
  background-color:transparent;
  cursor:default;
  padding-left:0;
  position:relative; }

.bp3-tree-node-content-0{
  padding-left:0px; }

.bp3-tree-node-content-1{
  padding-left:23px; }

.bp3-tree-node-content-2{
  padding-left:46px; }

.bp3-tree-node-content-3{
  padding-left:69px; }

.bp3-tree-node-content-4{
  padding-left:92px; }

.bp3-tree-node-content-5{
  padding-left:115px; }

.bp3-tree-node-content-6{
  padding-left:138px; }

.bp3-tree-node-content-7{
  padding-left:161px; }

.bp3-tree-node-content-8{
  padding-left:184px; }

.bp3-tree-node-content-9{
  padding-left:207px; }

.bp3-tree-node-content-10{
  padding-left:230px; }

.bp3-tree-node-content-11{
  padding-left:253px; }

.bp3-tree-node-content-12{
  padding-left:276px; }

.bp3-tree-node-content-13{
  padding-left:299px; }

.bp3-tree-node-content-14{
  padding-left:322px; }

.bp3-tree-node-content-15{
  padding-left:345px; }

.bp3-tree-node-content-16{
  padding-left:368px; }

.bp3-tree-node-content-17{
  padding-left:391px; }

.bp3-tree-node-content-18{
  padding-left:414px; }

.bp3-tree-node-content-19{
  padding-left:437px; }

.bp3-tree-node-content-20{
  padding-left:460px; }

.bp3-tree-node-content{
  -webkit-box-align:center;
      -ms-flex-align:center;
          align-items:center;
  display:-webkit-box;
  display:-ms-flexbox;
  display:flex;
  height:30px;
  padding-right:5px;
  width:100%; }
  .bp3-tree-node-content:hover{
    background-color:rgba(191, 204, 214, 0.4); }

.bp3-tree-node-caret,
.bp3-tree-node-caret-none{
  min-width:30px; }

.bp3-tree-node-caret{
  color:#5c7080;
  cursor:pointer;
  padding:7px;
  -webkit-transform:rotate(0deg);
          transform:rotate(0deg);
  -webkit-transition:-webkit-transform 200ms cubic-bezier(0.4, 1, 0.75, 0.9);
  transition:-webkit-transform 200ms cubic-bezier(0.4, 1, 0.75, 0.9);
  transition:transform 200ms cubic-bezier(0.4, 1, 0.75, 0.9);
  transition:transform 200ms cubic-bezier(0.4, 1, 0.75, 0.9), -webkit-transform 200ms cubic-bezier(0.4, 1, 0.75, 0.9); }
  .bp3-tree-node-caret:hover{
    color:#182026; }
  .bp3-dark .bp3-tree-node-caret{
    color:#a7b6c2; }
    .bp3-dark .bp3-tree-node-caret:hover{
      color:#f5f8fa; }
  .bp3-tree-node-caret.bp3-tree-node-caret-open{
    -webkit-transform:rotate(90deg);
            transform:rotate(90deg); }
  .bp3-tree-node-caret.bp3-icon-standard::before{
    content:""; }

.bp3-tree-node-icon{
  margin-right:7px;
  position:relative; }

.bp3-tree-node-label{
  overflow:hidden;
  text-overflow:ellipsis;
  white-space:nowrap;
  word-wrap:normal;
  -webkit-box-flex:1;
      -ms-flex:1 1 auto;
          flex:1 1 auto;
  position:relative;
  -webkit-user-select:none;
     -moz-user-select:none;
      -ms-user-select:none;
          user-select:none; }
  .bp3-tree-node-label span{
    display:inline; }

.bp3-tree-node-secondary-label{
  padding:0 5px;
  -webkit-user-select:none;
     -moz-user-select:none;
      -ms-user-select:none;
          user-select:none; }
  .bp3-tree-node-secondary-label .bp3-popover-wrapper,
  .bp3-tree-node-secondary-label .bp3-popover-target{
    -webkit-box-align:center;
        -ms-flex-align:center;
            align-items:center;
    display:-webkit-box;
    display:-ms-flexbox;
    display:flex; }

.bp3-tree-node.bp3-disabled .bp3-tree-node-content{
  background-color:inherit;
  color:rgba(92, 112, 128, 0.6);
  cursor:not-allowed; }

.bp3-tree-node.bp3-disabled .bp3-tree-node-caret,
.bp3-tree-node.bp3-disabled .bp3-tree-node-icon{
  color:rgba(92, 112, 128, 0.6);
  cursor:not-allowed; }

.bp3-tree-node.bp3-tree-node-selected > .bp3-tree-node-content{
  background-color:#137cbd; }
  .bp3-tree-node.bp3-tree-node-selected > .bp3-tree-node-content,
  .bp3-tree-node.bp3-tree-node-selected > .bp3-tree-node-content .bp3-icon, .bp3-tree-node.bp3-tree-node-selected > .bp3-tree-node-content .bp3-icon-standard, .bp3-tree-node.bp3-tree-node-selected > .bp3-tree-node-content .bp3-icon-large{
    color:#ffffff; }
  .bp3-tree-node.bp3-tree-node-selected > .bp3-tree-node-content .bp3-tree-node-caret::before{
    color:rgba(255, 255, 255, 0.7); }
  .bp3-tree-node.bp3-tree-node-selected > .bp3-tree-node-content .bp3-tree-node-caret:hover::before{
    color:#ffffff; }

.bp3-dark .bp3-tree-node-content:hover{
  background-color:rgba(92, 112, 128, 0.3); }

.bp3-dark .bp3-tree .bp3-icon, .bp3-dark .bp3-tree .bp3-icon-standard, .bp3-dark .bp3-tree .bp3-icon-large{
  color:#a7b6c2; }
  .bp3-dark .bp3-tree .bp3-icon.bp3-intent-primary, .bp3-dark .bp3-tree .bp3-icon-standard.bp3-intent-primary, .bp3-dark .bp3-tree .bp3-icon-large.bp3-intent-primary{
    color:#137cbd; }
  .bp3-dark .bp3-tree .bp3-icon.bp3-intent-success, .bp3-dark .bp3-tree .bp3-icon-standard.bp3-intent-success, .bp3-dark .bp3-tree .bp3-icon-large.bp3-intent-success{
    color:#0f9960; }
  .bp3-dark .bp3-tree .bp3-icon.bp3-intent-warning, .bp3-dark .bp3-tree .bp3-icon-standard.bp3-intent-warning, .bp3-dark .bp3-tree .bp3-icon-large.bp3-intent-warning{
    color:#d9822b; }
  .bp3-dark .bp3-tree .bp3-icon.bp3-intent-danger, .bp3-dark .bp3-tree .bp3-icon-standard.bp3-intent-danger, .bp3-dark .bp3-tree .bp3-icon-large.bp3-intent-danger{
    color:#db3737; }

.bp3-dark .bp3-tree-node.bp3-tree-node-selected > .bp3-tree-node-content{
  background-color:#137cbd; }
.bp3-omnibar{
  -webkit-filter:blur(0);
          filter:blur(0);
  opacity:1;
  background-color:#ffffff;
  border-radius:3px;
  -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 4px 8px rgba(16, 22, 26, 0.2), 0 18px 46px 6px rgba(16, 22, 26, 0.2);
          box-shadow:0 0 0 1px rgba(16, 22, 26, 0.1), 0 4px 8px rgba(16, 22, 26, 0.2), 0 18px 46px 6px rgba(16, 22, 26, 0.2);
  left:calc(50% - 250px);
  top:20vh;
  width:500px;
  z-index:21; }
  .bp3-omnibar.bp3-overlay-enter, .bp3-omnibar.bp3-overlay-appear{
    -webkit-filter:blur(20px);
            filter:blur(20px);
    opacity:0.2; }
  .bp3-omnibar.bp3-overlay-enter-active, .bp3-omnibar.bp3-overlay-appear-active{
    -webkit-filter:blur(0);
            filter:blur(0);
    opacity:1;
    -webkit-transition-delay:0;
            transition-delay:0;
    -webkit-transition-duration:200ms;
            transition-duration:200ms;
    -webkit-transition-property:opacity, -webkit-filter;
    transition-property:opacity, -webkit-filter;
    transition-property:filter, opacity;
    transition-property:filter, opacity, -webkit-filter;
    -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
            transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9); }
  .bp3-omnibar.bp3-overlay-exit{
    -webkit-filter:blur(0);
            filter:blur(0);
    opacity:1; }
  .bp3-omnibar.bp3-overlay-exit-active{
    -webkit-filter:blur(20px);
            filter:blur(20px);
    opacity:0.2;
    -webkit-transition-delay:0;
            transition-delay:0;
    -webkit-transition-duration:200ms;
            transition-duration:200ms;
    -webkit-transition-property:opacity, -webkit-filter;
    transition-property:opacity, -webkit-filter;
    transition-property:filter, opacity;
    transition-property:filter, opacity, -webkit-filter;
    -webkit-transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9);
            transition-timing-function:cubic-bezier(0.4, 1, 0.75, 0.9); }
  .bp3-omnibar .bp3-input{
    background-color:transparent;
    border-radius:0; }
    .bp3-omnibar .bp3-input, .bp3-omnibar .bp3-input:focus{
      -webkit-box-shadow:none;
              box-shadow:none; }
  .bp3-omnibar .bp3-menu{
    background-color:transparent;
    border-radius:0;
    -webkit-box-shadow:inset 0 1px 0 rgba(16, 22, 26, 0.15);
            box-shadow:inset 0 1px 0 rgba(16, 22, 26, 0.15);
    max-height:calc(60vh - 40px);
    overflow:auto; }
    .bp3-omnibar .bp3-menu:empty{
      display:none; }
  .bp3-dark .bp3-omnibar, .bp3-omnibar.bp3-dark{
    background-color:#30404d;
    -webkit-box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 4px 8px rgba(16, 22, 26, 0.4), 0 18px 46px 6px rgba(16, 22, 26, 0.4);
            box-shadow:0 0 0 1px rgba(16, 22, 26, 0.2), 0 4px 8px rgba(16, 22, 26, 0.4), 0 18px 46px 6px rgba(16, 22, 26, 0.4); }

.bp3-omnibar-overlay .bp3-overlay-backdrop{
  background-color:rgba(16, 22, 26, 0.2); }

.bp3-select-popover .bp3-popover-content{
  padding:5px; }

.bp3-select-popover .bp3-input-group{
  margin-bottom:0; }

.bp3-select-popover .bp3-menu{
  max-height:300px;
  max-width:400px;
  overflow:auto;
  padding:0; }
  .bp3-select-popover .bp3-menu:not(:first-child){
    padding-top:5px; }

.bp3-multi-select{
  min-width:150px; }

.bp3-multi-select-popover .bp3-menu{
  max-height:300px;
  max-width:400px;
  overflow:auto; }

.bp3-select-popover .bp3-popover-content{
  padding:5px; }

.bp3-select-popover .bp3-input-group{
  margin-bottom:0; }

.bp3-select-popover .bp3-menu{
  max-height:300px;
  max-width:400px;
  overflow:auto;
  padding:0; }
  .bp3-select-popover .bp3-menu:not(:first-child){
    padding-top:5px; }
/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/* This file was auto-generated by ensureUiComponents() in @jupyterlab/buildutils */

/**
 * (DEPRECATED) Support for consuming icons as CSS background images
 */

/* Icons urls */

:root {
  --jp-icon-add: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTE5IDEzaC02djZoLTJ2LTZINXYtMmg2VjVoMnY2aDZ2MnoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-bug: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIj4KICAgIDxwYXRoIGQ9Ik0yMCA4aC0yLjgxYy0uNDUtLjc4LTEuMDctMS40NS0xLjgyLTEuOTZMMTcgNC40MSAxNS41OSAzbC0yLjE3IDIuMTdDMTIuOTYgNS4wNiAxMi40OSA1IDEyIDVjLS40OSAwLS45Ni4wNi0xLjQxLjE3TDguNDEgMyA3IDQuNDFsMS42MiAxLjYzQzcuODggNi41NSA3LjI2IDcuMjIgNi44MSA4SDR2MmgyLjA5Yy0uMDUuMzMtLjA5LjY2LS4wOSAxdjFINHYyaDJ2MWMwIC4zNC4wNC42Ny4wOSAxSDR2MmgyLjgxYzEuMDQgMS43OSAyLjk3IDMgNS4xOSAzczQuMTUtMS4yMSA1LjE5LTNIMjB2LTJoLTIuMDljLjA1LS4zMy4wOS0uNjYuMDktMXYtMWgydi0yaC0ydi0xYzAtLjM0LS4wNC0uNjctLjA5LTFIMjBWOHptLTYgOGgtNHYtMmg0djJ6bTAtNGgtNHYtMmg0djJ6Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-build: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTYiIHZpZXdCb3g9IjAgMCAyNCAyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTE0LjkgMTcuNDVDMTYuMjUgMTcuNDUgMTcuMzUgMTYuMzUgMTcuMzUgMTVDMTcuMzUgMTMuNjUgMTYuMjUgMTIuNTUgMTQuOSAxMi41NUMxMy41NCAxMi41NSAxMi40NSAxMy42NSAxMi40NSAxNUMxMi40NSAxNi4zNSAxMy41NCAxNy40NSAxNC45IDE3LjQ1Wk0yMC4xIDE1LjY4TDIxLjU4IDE2Ljg0QzIxLjcxIDE2Ljk1IDIxLjc1IDE3LjEzIDIxLjY2IDE3LjI5TDIwLjI2IDE5LjcxQzIwLjE3IDE5Ljg2IDIwIDE5LjkyIDE5LjgzIDE5Ljg2TDE4LjA5IDE5LjE2QzE3LjczIDE5LjQ0IDE3LjMzIDE5LjY3IDE2LjkxIDE5Ljg1TDE2LjY0IDIxLjdDMTYuNjIgMjEuODcgMTYuNDcgMjIgMTYuMyAyMkgxMy41QzEzLjMyIDIyIDEzLjE4IDIxLjg3IDEzLjE1IDIxLjdMMTIuODkgMTkuODVDMTIuNDYgMTkuNjcgMTIuMDcgMTkuNDQgMTEuNzEgMTkuMTZMOS45NjAwMiAxOS44NkM5LjgxMDAyIDE5LjkyIDkuNjIwMDIgMTkuODYgOS41NDAwMiAxOS43MUw4LjE0MDAyIDE3LjI5QzguMDUwMDIgMTcuMTMgOC4wOTAwMiAxNi45NSA4LjIyMDAyIDE2Ljg0TDkuNzAwMDIgMTUuNjhMOS42NTAwMSAxNUw5LjcwMDAyIDE0LjMxTDguMjIwMDIgMTMuMTZDOC4wOTAwMiAxMy4wNSA4LjA1MDAyIDEyLjg2IDguMTQwMDIgMTIuNzFMOS41NDAwMiAxMC4yOUM5LjYyMDAyIDEwLjEzIDkuODEwMDIgMTAuMDcgOS45NjAwMiAxMC4xM0wxMS43MSAxMC44NEMxMi4wNyAxMC41NiAxMi40NiAxMC4zMiAxMi44OSAxMC4xNUwxMy4xNSA4LjI4OTk4QzEzLjE4IDguMTI5OTggMTMuMzIgNy45OTk5OCAxMy41IDcuOTk5OThIMTYuM0MxNi40NyA3Ljk5OTk4IDE2LjYyIDguMTI5OTggMTYuNjQgOC4yODk5OEwxNi45MSAxMC4xNUMxNy4zMyAxMC4zMiAxNy43MyAxMC41NiAxOC4wOSAxMC44NEwxOS44MyAxMC4xM0MyMCAxMC4wNyAyMC4xNyAxMC4xMyAyMC4yNiAxMC4yOUwyMS42NiAxMi43MUMyMS43NSAxMi44NiAyMS43MSAxMy4wNSAyMS41OCAxMy4xNkwyMC4xIDE0LjMxTDIwLjE1IDE1TDIwLjEgMTUuNjhaIi8+CiAgICA8cGF0aCBkPSJNNy4zMjk2NiA3LjQ0NDU0QzguMDgzMSA3LjAwOTU0IDguMzM5MzIgNi4wNTMzMiA3LjkwNDMyIDUuMjk5ODhDNy40NjkzMiA0LjU0NjQzIDYuNTA4MSA0LjI4MTU2IDUuNzU0NjYgNC43MTY1NkM1LjM5MTc2IDQuOTI2MDggNS4xMjY5NSA1LjI3MTE4IDUuMDE4NDkgNS42NzU5NEM0LjkxMDA0IDYuMDgwNzEgNC45NjY4MiA2LjUxMTk4IDUuMTc2MzQgNi44NzQ4OEM1LjYxMTM0IDcuNjI4MzIgNi41NzYyMiA3Ljg3OTU0IDcuMzI5NjYgNy40NDQ1NFpNOS42NTcxOCA0Ljc5NTkzTDEwLjg2NzIgNC45NTE3OUMxMC45NjI4IDQuOTc3NDEgMTEuMDQwMiA1LjA3MTMzIDExLjAzODIgNS4xODc5M0wxMS4wMzg4IDYuOTg4OTNDMTEuMDQ1NSA3LjEwMDU0IDEwLjk2MTYgNy4xOTUxOCAxMC44NTUgNy4yMTA1NEw5LjY2MDAxIDcuMzgwODNMOS4yMzkxNSA4LjEzMTg4TDkuNjY5NjEgOS4yNTc0NUM5LjcwNzI5IDkuMzYyNzEgOS42NjkzNCA5LjQ3Njk5IDkuNTc0MDggOS41MzE5OUw4LjAxNTIzIDEwLjQzMkM3LjkxMTMxIDEwLjQ5MiA3Ljc5MzM3IDEwLjQ2NzcgNy43MjEwNSAxMC4zODI0TDYuOTg3NDggOS40MzE4OEw2LjEwOTMxIDkuNDMwODNMNS4zNDcwNCAxMC4zOTA1QzUuMjg5MDkgMTAuNDcwMiA1LjE3MzgzIDEwLjQ5MDUgNS4wNzE4NyAxMC40MzM5TDMuNTEyNDUgOS41MzI5M0MzLjQxMDQ5IDkuNDc2MzMgMy4zNzY0NyA5LjM1NzQxIDMuNDEwNzUgOS4yNTY3OUwzLjg2MzQ3IDguMTQwOTNMMy42MTc0OSA3Ljc3NDg4TDMuNDIzNDcgNy4zNzg4M0wyLjIzMDc1IDcuMjEyOTdDMi4xMjY0NyA3LjE5MjM1IDIuMDQwNDkgNy4xMDM0MiAyLjA0MjQ1IDYuOTg2ODJMMi4wNDE4NyA1LjE4NTgyQzIuMDQzODMgNS4wNjkyMiAyLjExOTA5IDQuOTc5NTggMi4yMTcwNCA0Ljk2OTIyTDMuNDIwNjUgNC43OTM5M0wzLjg2NzQ5IDQuMDI3ODhMMy40MTEwNSAyLjkxNzMxQzMuMzczMzcgMi44MTIwNCAzLjQxMTMxIDIuNjk3NzYgMy41MTUyMyAyLjYzNzc2TDUuMDc0MDggMS43Mzc3NkM1LjE2OTM0IDEuNjgyNzYgNS4yODcyOSAxLjcwNzA0IDUuMzU5NjEgMS43OTIzMUw2LjExOTE1IDIuNzI3ODhMNi45ODAwMSAyLjczODkzTDcuNzI0OTYgMS43ODkyMkM3Ljc5MTU2IDEuNzA0NTggNy45MTU0OCAxLjY3OTIyIDguMDA4NzkgMS43NDA4Mkw5LjU2ODIxIDIuNjQxODJDOS42NzAxNyAyLjY5ODQyIDkuNzEyODUgMi44MTIzNCA5LjY4NzIzIDIuOTA3OTdMOS4yMTcxOCA0LjAzMzgzTDkuNDYzMTYgNC4zOTk4OEw5LjY1NzE4IDQuNzk1OTNaIi8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-caret-down-empty-thin: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIwIDIwIj4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSIgc2hhcGUtcmVuZGVyaW5nPSJnZW9tZXRyaWNQcmVjaXNpb24iPgoJCTxwb2x5Z29uIGNsYXNzPSJzdDEiIHBvaW50cz0iOS45LDEzLjYgMy42LDcuNCA0LjQsNi42IDkuOSwxMi4yIDE1LjQsNi43IDE2LjEsNy40ICIvPgoJPC9nPgo8L3N2Zz4K);
  --jp-icon-caret-down-empty: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiIHNoYXBlLXJlbmRlcmluZz0iZ2VvbWV0cmljUHJlY2lzaW9uIj4KICAgIDxwYXRoIGQ9Ik01LjIsNS45TDksOS43bDMuOC0zLjhsMS4yLDEuMmwtNC45LDVsLTQuOS01TDUuMiw1Ljl6Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-caret-down: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiIHNoYXBlLXJlbmRlcmluZz0iZ2VvbWV0cmljUHJlY2lzaW9uIj4KICAgIDxwYXRoIGQ9Ik01LjIsNy41TDksMTEuMmwzLjgtMy44SDUuMnoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-caret-left: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSIgc2hhcGUtcmVuZGVyaW5nPSJnZW9tZXRyaWNQcmVjaXNpb24iPgoJCTxwYXRoIGQ9Ik0xMC44LDEyLjhMNy4xLDlsMy44LTMuOGwwLDcuNkgxMC44eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-caret-right: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiIHNoYXBlLXJlbmRlcmluZz0iZ2VvbWV0cmljUHJlY2lzaW9uIj4KICAgIDxwYXRoIGQ9Ik03LjIsNS4yTDEwLjksOWwtMy44LDMuOFY1LjJINy4yeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-caret-up-empty-thin: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIwIDIwIj4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSIgc2hhcGUtcmVuZGVyaW5nPSJnZW9tZXRyaWNQcmVjaXNpb24iPgoJCTxwb2x5Z29uIGNsYXNzPSJzdDEiIHBvaW50cz0iMTUuNCwxMy4zIDkuOSw3LjcgNC40LDEzLjIgMy42LDEyLjUgOS45LDYuMyAxNi4xLDEyLjYgIi8+Cgk8L2c+Cjwvc3ZnPgo=);
  --jp-icon-caret-up: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSIgc2hhcGUtcmVuZGVyaW5nPSJnZW9tZXRyaWNQcmVjaXNpb24iPgoJCTxwYXRoIGQ9Ik01LjIsMTAuNUw5LDYuOGwzLjgsMy44SDUuMnoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-case-sensitive: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIwIDIwIj4KICA8ZyBjbGFzcz0ianAtaWNvbjIiIGZpbGw9IiM0MTQxNDEiPgogICAgPHJlY3QgeD0iMiIgeT0iMiIgd2lkdGg9IjE2IiBoZWlnaHQ9IjE2Ii8+CiAgPC9nPgogIDxnIGNsYXNzPSJqcC1pY29uLWFjY2VudDIiIGZpbGw9IiNGRkYiPgogICAgPHBhdGggZD0iTTcuNiw4aDAuOWwzLjUsOGgtMS4xTDEwLDE0SDZsLTAuOSwySDRMNy42LDh6IE04LDkuMUw2LjQsMTNoMy4yTDgsOS4xeiIvPgogICAgPHBhdGggZD0iTTE2LjYsOS44Yy0wLjIsMC4xLTAuNCwwLjEtMC43LDAuMWMtMC4yLDAtMC40LTAuMS0wLjYtMC4yYy0wLjEtMC4xLTAuMi0wLjQtMC4yLTAuNyBjLTAuMywwLjMtMC42LDAuNS0wLjksMC43Yy0wLjMsMC4xLTAuNywwLjItMS4xLDAuMmMtMC4zLDAtMC41LDAtMC43LTAuMWMtMC4yLTAuMS0wLjQtMC4yLTAuNi0wLjNjLTAuMi0wLjEtMC4zLTAuMy0wLjQtMC41IGMtMC4xLTAuMi0wLjEtMC40LTAuMS0wLjdjMC0wLjMsMC4xLTAuNiwwLjItMC44YzAuMS0wLjIsMC4zLTAuNCwwLjQtMC41QzEyLDcsMTIuMiw2LjksMTIuNSw2LjhjMC4yLTAuMSwwLjUtMC4xLDAuNy0wLjIgYzAuMy0wLjEsMC41LTAuMSwwLjctMC4xYzAuMiwwLDAuNC0wLjEsMC42LTAuMWMwLjIsMCwwLjMtMC4xLDAuNC0wLjJjMC4xLTAuMSwwLjItMC4yLDAuMi0wLjRjMC0xLTEuMS0xLTEuMy0xIGMtMC40LDAtMS40LDAtMS40LDEuMmgtMC45YzAtMC40LDAuMS0wLjcsMC4yLTFjMC4xLTAuMiwwLjMtMC40LDAuNS0wLjZjMC4yLTAuMiwwLjUtMC4zLDAuOC0wLjNDMTMuMyw0LDEzLjYsNCwxMy45LDQgYzAuMywwLDAuNSwwLDAuOCwwLjFjMC4zLDAsMC41LDAuMSwwLjcsMC4yYzAuMiwwLjEsMC40LDAuMywwLjUsMC41QzE2LDUsMTYsNS4yLDE2LDUuNnYyLjljMCwwLjIsMCwwLjQsMCwwLjUgYzAsMC4xLDAuMSwwLjIsMC4zLDAuMmMwLjEsMCwwLjIsMCwwLjMsMFY5Ljh6IE0xNS4yLDYuOWMtMS4yLDAuNi0zLjEsMC4yLTMuMSwxLjRjMCwxLjQsMy4xLDEsMy4xLTAuNVY2Ljl6Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-check: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIj4KICAgIDxwYXRoIGQ9Ik05IDE2LjE3TDQuODMgMTJsLTEuNDIgMS40MUw5IDE5IDIxIDdsLTEuNDEtMS40MXoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-circle-empty: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTEyIDJDNi40NyAyIDIgNi40NyAyIDEyczQuNDcgMTAgMTAgMTAgMTAtNC40NyAxMC0xMFMxNy41MyAyIDEyIDJ6bTAgMThjLTQuNDEgMC04LTMuNTktOC04czMuNTktOCA4LTggOCAzLjU5IDggOC0zLjU5IDgtOCA4eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-circle: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMTggMTgiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPGNpcmNsZSBjeD0iOSIgY3k9IjkiIHI9IjgiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-clear: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8bWFzayBpZD0iZG9udXRIb2xlIj4KICAgIDxyZWN0IHdpZHRoPSIyNCIgaGVpZ2h0PSIyNCIgZmlsbD0id2hpdGUiIC8+CiAgICA8Y2lyY2xlIGN4PSIxMiIgY3k9IjEyIiByPSI4IiBmaWxsPSJibGFjayIvPgogIDwvbWFzaz4KCiAgPGcgY2xhc3M9ImpwLWljb24zIiBmaWxsPSIjNjE2MTYxIj4KICAgIDxyZWN0IGhlaWdodD0iMTgiIHdpZHRoPSIyIiB4PSIxMSIgeT0iMyIgdHJhbnNmb3JtPSJyb3RhdGUoMzE1LCAxMiwgMTIpIi8+CiAgICA8Y2lyY2xlIGN4PSIxMiIgY3k9IjEyIiByPSIxMCIgbWFzaz0idXJsKCNkb251dEhvbGUpIi8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-close: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbi1ub25lIGpwLWljb24tc2VsZWN0YWJsZS1pbnZlcnNlIGpwLWljb24zLWhvdmVyIiBmaWxsPSJub25lIj4KICAgIDxjaXJjbGUgY3g9IjEyIiBjeT0iMTIiIHI9IjExIi8+CiAgPC9nPgoKICA8ZyBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIGpwLWljb24tYWNjZW50Mi1ob3ZlciIgZmlsbD0iIzYxNjE2MSI+CiAgICA8cGF0aCBkPSJNMTkgNi40MUwxNy41OSA1IDEyIDEwLjU5IDYuNDEgNSA1IDYuNDEgMTAuNTkgMTIgNSAxNy41OSA2LjQxIDE5IDEyIDEzLjQxIDE3LjU5IDE5IDE5IDE3LjU5IDEzLjQxIDEyeiIvPgogIDwvZz4KCiAgPGcgY2xhc3M9ImpwLWljb24tbm9uZSBqcC1pY29uLWJ1c3kiIGZpbGw9Im5vbmUiPgogICAgPGNpcmNsZSBjeD0iMTIiIGN5PSIxMiIgcj0iNyIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-code: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjIiIGhlaWdodD0iMjIiIHZpZXdCb3g9IjAgMCAyOCAyOCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CgkJPHBhdGggZD0iTTExLjQgMTguNkw2LjggMTRMMTEuNCA5LjRMMTAgOEw0IDE0TDEwIDIwTDExLjQgMTguNlpNMTYuNiAxOC42TDIxLjIgMTRMMTYuNiA5LjRMMTggOEwyNCAxNEwxOCAyMEwxNi42IDE4LjZWMTguNloiLz4KCTwvZz4KPC9zdmc+Cg==);
  --jp-icon-console: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIwMCAyMDAiPgogIDxnIGNsYXNzPSJqcC1pY29uLWJyYW5kMSBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiMwMjg4RDEiPgogICAgPHBhdGggZD0iTTIwIDE5LjhoMTYwdjE1OS45SDIweiIvPgogIDwvZz4KICA8ZyBjbGFzcz0ianAtaWNvbi1zZWxlY3RhYmxlLWludmVyc2UiIGZpbGw9IiNmZmYiPgogICAgPHBhdGggZD0iTTEwNSAxMjcuM2g0MHYxMi44aC00MHpNNTEuMSA3N0w3NCA5OS45bC0yMy4zIDIzLjMgMTAuNSAxMC41IDIzLjMtMjMuM0w5NSA5OS45IDg0LjUgODkuNCA2MS42IDY2LjV6Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-copy: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMTggMTgiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTExLjksMUgzLjJDMi40LDEsMS43LDEuNywxLjcsMi41djEwLjJoMS41VjIuNWg4LjdWMXogTTE0LjEsMy45aC04Yy0wLjgsMC0xLjUsMC43LTEuNSwxLjV2MTAuMmMwLDAuOCwwLjcsMS41LDEuNSwxLjVoOCBjMC44LDAsMS41LTAuNywxLjUtMS41VjUuNEMxNS41LDQuNiwxNC45LDMuOSwxNC4xLDMuOXogTTE0LjEsMTUuNWgtOFY1LjRoOFYxNS41eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-copyright: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIGVuYWJsZS1iYWNrZ3JvdW5kPSJuZXcgMCAwIDI0IDI0IiBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCI+CiAgPGcgY2xhc3M9ImpwLWljb24zIiBmaWxsPSIjNjE2MTYxIj4KICAgIDxwYXRoIGQ9Ik0xMS44OCw5LjE0YzEuMjgsMC4wNiwxLjYxLDEuMTUsMS42MywxLjY2aDEuNzljLTAuMDgtMS45OC0xLjQ5LTMuMTktMy40NS0zLjE5QzkuNjQsNy42MSw4LDksOCwxMi4xNCBjMCwxLjk0LDAuOTMsNC4yNCwzLjg0LDQuMjRjMi4yMiwwLDMuNDEtMS42NSwzLjQ0LTIuOTVoLTEuNzljLTAuMDMsMC41OS0wLjQ1LDEuMzgtMS42MywxLjQ0QzEwLjU1LDE0LjgzLDEwLDEzLjgxLDEwLDEyLjE0IEMxMCw5LjI1LDExLjI4LDkuMTYsMTEuODgsOS4xNHogTTEyLDJDNi40OCwyLDIsNi40OCwyLDEyczQuNDgsMTAsMTAsMTBzMTAtNC40OCwxMC0xMFMxNy41MiwyLDEyLDJ6IE0xMiwyMGMtNC40MSwwLTgtMy41OS04LTggczMuNTktOCw4LThzOCwzLjU5LDgsOFMxNi40MSwyMCwxMiwyMHoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-cut: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTkuNjQgNy42NGMuMjMtLjUuMzYtMS4wNS4zNi0xLjY0IDAtMi4yMS0xLjc5LTQtNC00UzIgMy43OSAyIDZzMS43OSA0IDQgNGMuNTkgMCAxLjE0LS4xMyAxLjY0LS4zNkwxMCAxMmwtMi4zNiAyLjM2QzcuMTQgMTQuMTMgNi41OSAxNCA2IDE0Yy0yLjIxIDAtNCAxLjc5LTQgNHMxLjc5IDQgNCA0IDQtMS43OSA0LTRjMC0uNTktLjEzLTEuMTQtLjM2LTEuNjRMMTIgMTRsNyA3aDN2LTFMOS42NCA3LjY0ek02IDhjLTEuMSAwLTItLjg5LTItMnMuOS0yIDItMiAyIC44OSAyIDItLjkgMi0yIDJ6bTAgMTJjLTEuMSAwLTItLjg5LTItMnMuOS0yIDItMiAyIC44OSAyIDItLjkgMi0yIDJ6bTYtNy41Yy0uMjggMC0uNS0uMjItLjUtLjVzLjIyLS41LjUtLjUuNS4yMi41LjUtLjIyLjUtLjUuNXpNMTkgM2wtNiA2IDIgMiA3LTdWM3oiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-download: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTE5IDloLTRWM0g5djZINWw3IDcgNy03ek01IDE4djJoMTR2LTJINXoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-edit: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTMgMTcuMjVWMjFoMy43NUwxNy44MSA5Ljk0bC0zLjc1LTMuNzVMMyAxNy4yNXpNMjAuNzEgNy4wNGMuMzktLjM5LjM5LTEuMDIgMC0xLjQxbC0yLjM0LTIuMzRjLS4zOS0uMzktMS4wMi0uMzktMS40MSAwbC0xLjgzIDEuODMgMy43NSAzLjc1IDEuODMtMS44M3oiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-ellipses: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPGNpcmNsZSBjeD0iNSIgY3k9IjEyIiByPSIyIi8+CiAgICA8Y2lyY2xlIGN4PSIxMiIgY3k9IjEyIiByPSIyIi8+CiAgICA8Y2lyY2xlIGN4PSIxOSIgY3k9IjEyIiByPSIyIi8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-extension: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTIwLjUgMTFIMTlWN2MwLTEuMS0uOS0yLTItMmgtNFYzLjVDMTMgMi4xMiAxMS44OCAxIDEwLjUgMVM4IDIuMTIgOCAzLjVWNUg0Yy0xLjEgMC0xLjk5LjktMS45OSAydjMuOEgzLjVjMS40OSAwIDIuNyAxLjIxIDIuNyAyLjdzLTEuMjEgMi43LTIuNyAyLjdIMlYyMGMwIDEuMS45IDIgMiAyaDMuOHYtMS41YzAtMS40OSAxLjIxLTIuNyAyLjctMi43IDEuNDkgMCAyLjcgMS4yMSAyLjcgMi43VjIySDE3YzEuMSAwIDItLjkgMi0ydi00aDEuNWMxLjM4IDAgMi41LTEuMTIgMi41LTIuNVMyMS44OCAxMSAyMC41IDExeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-fast-forward: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIyNCIgaGVpZ2h0PSIyNCIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTQgMThsOC41LTZMNCA2djEyem05LTEydjEybDguNS02TDEzIDZ6Ii8+CiAgICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-file-upload: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTkgMTZoNnYtNmg0bC03LTctNyA3aDR6bS00IDJoMTR2Mkg1eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-file: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8cGF0aCBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMTkuMyA4LjJsLTUuNS01LjVjLS4zLS4zLS43LS41LTEuMi0uNUgzLjljLS44LjEtMS42LjktMS42IDEuOHYxNC4xYzAgLjkuNyAxLjYgMS42IDEuNmgxNC4yYy45IDAgMS42LS43IDEuNi0xLjZWOS40Yy4xLS41LS4xLS45LS40LTEuMnptLTUuOC0zLjNsMy40IDMuNmgtMy40VjQuOXptMy45IDEyLjdINC43Yy0uMSAwLS4yIDAtLjItLjJWNC43YzAtLjIuMS0uMy4yLS4zaDcuMnY0LjRzMCAuOC4zIDEuMWMuMy4zIDEuMS4zIDEuMS4zaDQuM3Y3LjJzLS4xLjItLjIuMnoiLz4KPC9zdmc+Cg==);
  --jp-icon-filter-list: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTEwIDE4aDR2LTJoLTR2MnpNMyA2djJoMThWNkgzem0zIDdoMTJ2LTJINnYyeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-folder: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMTAgNEg0Yy0xLjEgMC0xLjk5LjktMS45OSAyTDIgMThjMCAxLjEuOSAyIDIgMmgxNmMxLjEgMCAyLS45IDItMlY4YzAtMS4xLS45LTItMi0yaC04bC0yLTJ6Ii8+Cjwvc3ZnPgo=);
  --jp-icon-html5: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDUxMiA1MTIiPgogIDxwYXRoIGNsYXNzPSJqcC1pY29uMCBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiMwMDAiIGQ9Ik0xMDguNCAwaDIzdjIyLjhoMjEuMlYwaDIzdjY5aC0yM1Y0NmgtMjF2MjNoLTIzLjJNMjA2IDIzaC0yMC4zVjBoNjMuN3YyM0gyMjl2NDZoLTIzbTUzLjUtNjloMjQuMWwxNC44IDI0LjNMMzEzLjIgMGgyNC4xdjY5aC0yM1YzNC44bC0xNi4xIDI0LjgtMTYuMS0yNC44VjY5aC0yMi42bTg5LjItNjloMjN2NDYuMmgzMi42VjY5aC01NS42Ii8+CiAgPHBhdGggY2xhc3M9ImpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iI2U0NGQyNiIgZD0iTTEwNy42IDQ3MWwtMzMtMzcwLjRoMzYyLjhsLTMzIDM3MC4yTDI1NS43IDUxMiIvPgogIDxwYXRoIGNsYXNzPSJqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiNmMTY1MjkiIGQ9Ik0yNTYgNDgwLjVWMTMxaDE0OC4zTDM3NiA0NDciLz4KICA8cGF0aCBjbGFzcz0ianAtaWNvbi1zZWxlY3RhYmxlLWludmVyc2UiIGZpbGw9IiNlYmViZWIiIGQ9Ik0xNDIgMTc2LjNoMTE0djQ1LjRoLTY0LjJsNC4yIDQ2LjVoNjB2NDUuM0gxNTQuNG0yIDIyLjhIMjAybDMuMiAzNi4zIDUwLjggMTMuNnY0Ny40bC05My4yLTI2Ii8+CiAgPHBhdGggY2xhc3M9ImpwLWljb24tc2VsZWN0YWJsZS1pbnZlcnNlIiBmaWxsPSIjZmZmIiBkPSJNMzY5LjYgMTc2LjNIMjU1Ljh2NDUuNGgxMDkuNm0tNC4xIDQ2LjVIMjU1Ljh2NDUuNGg1NmwtNS4zIDU5LTUwLjcgMTMuNnY0Ny4ybDkzLTI1LjgiLz4KPC9zdmc+Cg==);
  --jp-icon-image: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8cGF0aCBjbGFzcz0ianAtaWNvbi1icmFuZDQganAtaWNvbi1zZWxlY3RhYmxlLWludmVyc2UiIGZpbGw9IiNGRkYiIGQ9Ik0yLjIgMi4yaDE3LjV2MTcuNUgyLjJ6Ii8+CiAgPHBhdGggY2xhc3M9ImpwLWljb24tYnJhbmQwIGpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iIzNGNTFCNSIgZD0iTTIuMiAyLjJ2MTcuNWgxNy41bC4xLTE3LjVIMi4yem0xMi4xIDIuMmMxLjIgMCAyLjIgMSAyLjIgMi4ycy0xIDIuMi0yLjIgMi4yLTIuMi0xLTIuMi0yLjIgMS0yLjIgMi4yLTIuMnpNNC40IDE3LjZsMy4zLTguOCAzLjMgNi42IDIuMi0zLjIgNC40IDUuNEg0LjR6Ii8+Cjwvc3ZnPgo=);
  --jp-icon-inspector: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMjAgNEg0Yy0xLjEgMC0xLjk5LjktMS45OSAyTDIgMThjMCAxLjEuOSAyIDIgMmgxNmMxLjEgMCAyLS45IDItMlY2YzAtMS4xLS45LTItMi0yem0tNSAxNEg0di00aDExdjR6bTAtNUg0VjloMTF2NHptNSA1aC00VjloNHY5eiIvPgo8L3N2Zz4K);
  --jp-icon-json: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8ZyBjbGFzcz0ianAtaWNvbi13YXJuMSBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiNGOUE4MjUiPgogICAgPHBhdGggZD0iTTIwLjIgMTEuOGMtMS42IDAtMS43LjUtMS43IDEgMCAuNC4xLjkuMSAxLjMuMS41LjEuOS4xIDEuMyAwIDEuNy0xLjQgMi4zLTMuNSAyLjNoLS45di0xLjloLjVjMS4xIDAgMS40IDAgMS40LS44IDAtLjMgMC0uNi0uMS0xIDAtLjQtLjEtLjgtLjEtMS4yIDAtMS4zIDAtMS44IDEuMy0yLTEuMy0uMi0xLjMtLjctMS4zLTIgMC0uNC4xLS44LjEtMS4yLjEtLjQuMS0uNy4xLTEgMC0uOC0uNC0uNy0xLjQtLjhoLS41VjQuMWguOWMyLjIgMCAzLjUuNyAzLjUgMi4zIDAgLjQtLjEuOS0uMSAxLjMtLjEuNS0uMS45LS4xIDEuMyAwIC41LjIgMSAxLjcgMXYxLjh6TTEuOCAxMC4xYzEuNiAwIDEuNy0uNSAxLjctMSAwLS40LS4xLS45LS4xLTEuMy0uMS0uNS0uMS0uOS0uMS0xLjMgMC0xLjYgMS40LTIuMyAzLjUtMi4zaC45djEuOWgtLjVjLTEgMC0xLjQgMC0xLjQuOCAwIC4zIDAgLjYuMSAxIDAgLjIuMS42LjEgMSAwIDEuMyAwIDEuOC0xLjMgMkM2IDExLjIgNiAxMS43IDYgMTNjMCAuNC0uMS44LS4xIDEuMi0uMS4zLS4xLjctLjEgMSAwIC44LjMuOCAxLjQuOGguNXYxLjloLS45Yy0yLjEgMC0zLjUtLjYtMy41LTIuMyAwLS40LjEtLjkuMS0xLjMuMS0uNS4xLS45LjEtMS4zIDAtLjUtLjItMS0xLjctMXYtMS45eiIvPgogICAgPGNpcmNsZSBjeD0iMTEiIGN5PSIxMy44IiByPSIyLjEiLz4KICAgIDxjaXJjbGUgY3g9IjExIiBjeT0iOC4yIiByPSIyLjEiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-julia: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDMyNSAzMDAiPgogIDxnIGNsYXNzPSJqcC1icmFuZDAganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjY2IzYzMzIj4KICAgIDxwYXRoIGQ9Ik0gMTUwLjg5ODQzOCAyMjUgQyAxNTAuODk4NDM4IDI2Ni40MjE4NzUgMTE3LjMyMDMxMiAzMDAgNzUuODk4NDM4IDMwMCBDIDM0LjQ3NjU2MiAzMDAgMC44OTg0MzggMjY2LjQyMTg3NSAwLjg5ODQzOCAyMjUgQyAwLjg5ODQzOCAxODMuNTc4MTI1IDM0LjQ3NjU2MiAxNTAgNzUuODk4NDM4IDE1MCBDIDExNy4zMjAzMTIgMTUwIDE1MC44OTg0MzggMTgzLjU3ODEyNSAxNTAuODk4NDM4IDIyNSIvPgogIDwvZz4KICA8ZyBjbGFzcz0ianAtYnJhbmQwIGpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iIzM4OTgyNiI+CiAgICA8cGF0aCBkPSJNIDIzNy41IDc1IEMgMjM3LjUgMTE2LjQyMTg3NSAyMDMuOTIxODc1IDE1MCAxNjIuNSAxNTAgQyAxMjEuMDc4MTI1IDE1MCA4Ny41IDExNi40MjE4NzUgODcuNSA3NSBDIDg3LjUgMzMuNTc4MTI1IDEyMS4wNzgxMjUgMCAxNjIuNSAwIEMgMjAzLjkyMTg3NSAwIDIzNy41IDMzLjU3ODEyNSAyMzcuNSA3NSIvPgogIDwvZz4KICA8ZyBjbGFzcz0ianAtYnJhbmQwIGpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iIzk1NThiMiI+CiAgICA8cGF0aCBkPSJNIDMyNC4xMDE1NjIgMjI1IEMgMzI0LjEwMTU2MiAyNjYuNDIxODc1IDI5MC41MjM0MzggMzAwIDI0OS4xMDE1NjIgMzAwIEMgMjA3LjY3OTY4OCAzMDAgMTc0LjEwMTU2MiAyNjYuNDIxODc1IDE3NC4xMDE1NjIgMjI1IEMgMTc0LjEwMTU2MiAxODMuNTc4MTI1IDIwNy42Nzk2ODggMTUwIDI0OS4xMDE1NjIgMTUwIEMgMjkwLjUyMzQzOCAxNTAgMzI0LjEwMTU2MiAxODMuNTc4MTI1IDMyNC4xMDE1NjIgMjI1Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-jupyter-favicon: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTUyIiBoZWlnaHQ9IjE2NSIgdmlld0JveD0iMCAwIDE1MiAxNjUiIHZlcnNpb249IjEuMSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbi13YXJuMCIgZmlsbD0iI0YzNzcyNiI+CiAgICA8cGF0aCB0cmFuc2Zvcm09InRyYW5zbGF0ZSgwLjA3ODk0NywgMTEwLjU4MjkyNykiIGQ9Ik03NS45NDIyODQyLDI5LjU4MDQ1NjEgQzQzLjMwMjM5NDcsMjkuNTgwNDU2MSAxNC43OTY3ODMyLDE3LjY1MzQ2MzQgMCwwIEM1LjUxMDgzMjExLDE1Ljg0MDY4MjkgMTUuNzgxNTM4OSwyOS41NjY3NzMyIDI5LjM5MDQ5NDcsMzkuMjc4NDE3MSBDNDIuOTk5Nyw0OC45ODk4NTM3IDU5LjI3MzcsNTQuMjA2NzgwNSA3NS45NjA1Nzg5LDU0LjIwNjc4MDUgQzkyLjY0NzQ1NzksNTQuMjA2NzgwNSAxMDguOTIxNDU4LDQ4Ljk4OTg1MzcgMTIyLjUzMDY2MywzOS4yNzg0MTcxIEMxMzYuMTM5NDUzLDI5LjU2Njc3MzIgMTQ2LjQxMDI4NCwxNS44NDA2ODI5IDE1MS45MjExNTgsMCBDMTM3LjA4Nzg2OCwxNy42NTM0NjM0IDEwOC41ODI1ODksMjkuNTgwNDU2MSA3NS45NDIyODQyLDI5LjU4MDQ1NjEgTDc1Ljk0MjI4NDIsMjkuNTgwNDU2MSBaIiAvPgogICAgPHBhdGggdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMC4wMzczNjgsIDAuNzA0ODc4KSIgZD0iTTc1Ljk3ODQ1NzksMjQuNjI2NDA3MyBDMTA4LjYxODc2MywyNC42MjY0MDczIDEzNy4xMjQ0NTgsMzYuNTUzNDQxNSAxNTEuOTIxMTU4LDU0LjIwNjc4MDUgQzE0Ni40MTAyODQsMzguMzY2MjIyIDEzNi4xMzk0NTMsMjQuNjQwMTMxNyAxMjIuNTMwNjYzLDE0LjkyODQ4NzggQzEwOC45MjE0NTgsNS4yMTY4NDM5IDkyLjY0NzQ1NzksMCA3NS45NjA1Nzg5LDAgQzU5LjI3MzcsMCA0Mi45OTk3LDUuMjE2ODQzOSAyOS4zOTA0OTQ3LDE0LjkyODQ4NzggQzE1Ljc4MTUzODksMjQuNjQwMTMxNyA1LjUxMDgzMjExLDM4LjM2NjIyMiAwLDU0LjIwNjc4MDUgQzE0LjgzMzA4MTYsMzYuNTg5OTI5MyA0My4zMzg1Njg0LDI0LjYyNjQwNzMgNzUuOTc4NDU3OSwyNC42MjY0MDczIEw3NS45Nzg0NTc5LDI0LjYyNjQwNzMgWiIgLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-jupyter: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMzkiIGhlaWdodD0iNTEiIHZpZXdCb3g9IjAgMCAzOSA1MSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMTYzOCAtMjI4MSkiPgogICAgPGcgY2xhc3M9ImpwLWljb24td2FybjAiIGZpbGw9IiNGMzc3MjYiPgogICAgICA8cGF0aCB0cmFuc2Zvcm09InRyYW5zbGF0ZSgxNjM5Ljc0IDIzMTEuOTgpIiBkPSJNIDE4LjI2NDYgNy4xMzQxMUMgMTAuNDE0NSA3LjEzNDExIDMuNTU4NzIgNC4yNTc2IDAgMEMgMS4zMjUzOSAzLjgyMDQgMy43OTU1NiA3LjEzMDgxIDcuMDY4NiA5LjQ3MzAzQyAxMC4zNDE3IDExLjgxNTIgMTQuMjU1NyAxMy4wNzM0IDE4LjI2OSAxMy4wNzM0QyAyMi4yODIzIDEzLjA3MzQgMjYuMTk2MyAxMS44MTUyIDI5LjQ2OTQgOS40NzMwM0MgMzIuNzQyNCA3LjEzMDgxIDM1LjIxMjYgMy44MjA0IDM2LjUzOCAwQyAzMi45NzA1IDQuMjU3NiAyNi4xMTQ4IDcuMTM0MTEgMTguMjY0NiA3LjEzNDExWiIvPgogICAgICA8cGF0aCB0cmFuc2Zvcm09InRyYW5zbGF0ZSgxNjM5LjczIDIyODUuNDgpIiBkPSJNIDE4LjI3MzMgNS45MzkzMUMgMjYuMTIzNSA1LjkzOTMxIDMyLjk3OTMgOC44MTU4MyAzNi41MzggMTMuMDczNEMgMzUuMjEyNiA5LjI1MzAzIDMyLjc0MjQgNS45NDI2MiAyOS40Njk0IDMuNjAwNEMgMjYuMTk2MyAxLjI1ODE4IDIyLjI4MjMgMCAxOC4yNjkgMEMgMTQuMjU1NyAwIDEwLjM0MTcgMS4yNTgxOCA3LjA2ODYgMy42MDA0QyAzLjc5NTU2IDUuOTQyNjIgMS4zMjUzOSA5LjI1MzAzIDAgMTMuMDczNEMgMy41Njc0NSA4LjgyNDYzIDEwLjQyMzIgNS45MzkzMSAxOC4yNzMzIDUuOTM5MzFaIi8+CiAgICA8L2c+CiAgICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgICA8cGF0aCB0cmFuc2Zvcm09InRyYW5zbGF0ZSgxNjY5LjMgMjI4MS4zMSkiIGQ9Ik0gNS44OTM1MyAyLjg0NEMgNS45MTg4OSAzLjQzMTY1IDUuNzcwODUgNC4wMTM2NyA1LjQ2ODE1IDQuNTE2NDVDIDUuMTY1NDUgNS4wMTkyMiA0LjcyMTY4IDUuNDIwMTUgNC4xOTI5OSA1LjY2ODUxQyAzLjY2NDMgNS45MTY4OCAzLjA3NDQ0IDYuMDAxNTEgMi40OTgwNSA1LjkxMTcxQyAxLjkyMTY2IDUuODIxOSAxLjM4NDYzIDUuNTYxNyAwLjk1NDg5OCA1LjE2NDAxQyAwLjUyNTE3IDQuNzY2MzMgMC4yMjIwNTYgNC4yNDkwMyAwLjA4MzkwMzcgMy42Nzc1N0MgLTAuMDU0MjQ4MyAzLjEwNjExIC0wLjAyMTIzIDIuNTA2MTcgMC4xNzg3ODEgMS45NTM2NEMgMC4zNzg3OTMgMS40MDExIDAuNzM2ODA5IDAuOTIwODE3IDEuMjA3NTQgMC41NzM1MzhDIDEuNjc4MjYgMC4yMjYyNTkgMi4yNDA1NSAwLjAyNzU5MTkgMi44MjMyNiAwLjAwMjY3MjI5QyAzLjYwMzg5IC0wLjAzMDcxMTUgNC4zNjU3MyAwLjI0OTc4OSA0Ljk0MTQyIDAuNzgyNTUxQyA1LjUxNzExIDEuMzE1MzEgNS44NTk1NiAyLjA1Njc2IDUuODkzNTMgMi44NDRaIi8+CiAgICAgIDxwYXRoIHRyYW5zZm9ybT0idHJhbnNsYXRlKDE2MzkuOCAyMzIzLjgxKSIgZD0iTSA3LjQyNzg5IDMuNTgzMzhDIDcuNDYwMDggNC4zMjQzIDcuMjczNTUgNS4wNTgxOSA2Ljg5MTkzIDUuNjkyMTNDIDYuNTEwMzEgNi4zMjYwNyA1Ljk1MDc1IDYuODMxNTYgNS4yODQxMSA3LjE0NDZDIDQuNjE3NDcgNy40NTc2MyAzLjg3MzcxIDcuNTY0MTQgMy4xNDcwMiA3LjQ1MDYzQyAyLjQyMDMyIDcuMzM3MTIgMS43NDMzNiA3LjAwODcgMS4yMDE4NCA2LjUwNjk1QyAwLjY2MDMyOCA2LjAwNTIgMC4yNzg2MSA1LjM1MjY4IDAuMTA1MDE3IDQuNjMyMDJDIC0wLjA2ODU3NTcgMy45MTEzNSAtMC4wMjYyMzYxIDMuMTU0OTQgMC4yMjY2NzUgMi40NTg1NkMgMC40Nzk1ODcgMS43NjIxNyAwLjkzMTY5NyAxLjE1NzEzIDEuNTI1NzYgMC43MjAwMzNDIDIuMTE5ODMgMC4yODI5MzUgMi44MjkxNCAwLjAzMzQzOTUgMy41NjM4OSAwLjAwMzEzMzQ0QyA0LjU0NjY3IC0wLjAzNzQwMzMgNS41MDUyOSAwLjMxNjcwNiA2LjIyOTYxIDAuOTg3ODM1QyA2Ljk1MzkzIDEuNjU4OTYgNy4zODQ4NCAyLjU5MjM1IDcuNDI3ODkgMy41ODMzOEwgNy40Mjc4OSAzLjU4MzM4WiIvPgogICAgICA8cGF0aCB0cmFuc2Zvcm09InRyYW5zbGF0ZSgxNjM4LjM2IDIyODYuMDYpIiBkPSJNIDIuMjc0NzEgNC4zOTYyOUMgMS44NDM2MyA0LjQxNTA4IDEuNDE2NzEgNC4zMDQ0NSAxLjA0Nzk5IDQuMDc4NDNDIDAuNjc5MjY4IDMuODUyNCAwLjM4NTMyOCAzLjUyMTE0IDAuMjAzMzcxIDMuMTI2NTZDIDAuMDIxNDEzNiAyLjczMTk4IC0wLjA0MDM3OTggMi4yOTE4MyAwLjAyNTgxMTYgMS44NjE4MUMgMC4wOTIwMDMxIDEuNDMxOCAwLjI4MzIwNCAxLjAzMTI2IDAuNTc1MjEzIDAuNzEwODgzQyAwLjg2NzIyMiAwLjM5MDUxIDEuMjQ2OTEgMC4xNjQ3MDggMS42NjYyMiAwLjA2MjA1OTJDIDIuMDg1NTMgLTAuMDQwNTg5NyAyLjUyNTYxIC0wLjAxNTQ3MTQgMi45MzA3NiAwLjEzNDIzNUMgMy4zMzU5MSAwLjI4Mzk0MSAzLjY4NzkyIDAuNTUxNTA1IDMuOTQyMjIgMC45MDMwNkMgNC4xOTY1MiAxLjI1NDYyIDQuMzQxNjkgMS42NzQzNiA0LjM1OTM1IDIuMTA5MTZDIDQuMzgyOTkgMi42OTEwNyA0LjE3Njc4IDMuMjU4NjkgMy43ODU5NyAzLjY4NzQ2QyAzLjM5NTE2IDQuMTE2MjQgMi44NTE2NiA0LjM3MTE2IDIuMjc0NzEgNC4zOTYyOUwgMi4yNzQ3MSA0LjM5NjI5WiIvPgogICAgPC9nPgogIDwvZz4+Cjwvc3ZnPgo=);
  --jp-icon-jupyterlab-wordmark: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIyMDAiIHZpZXdCb3g9IjAgMCAxODYwLjggNDc1Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjIiIGZpbGw9IiM0RTRFNEUiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDQ4MC4xMzY0MDEsIDY0LjI3MTQ5MykiPgogICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMC4wMDAwMDAsIDU4Ljg3NTU2NikiPgogICAgICA8ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgwLjA4NzYwMywgMC4xNDAyOTQpIj4KICAgICAgICA8cGF0aCBkPSJNLTQyNi45LDE2OS44YzAsNDguNy0zLjcsNjQuNy0xMy42LDc2LjRjLTEwLjgsMTAtMjUsMTUuNS0zOS43LDE1LjVsMy43LDI5IGMyMi44LDAuMyw0NC44LTcuOSw2MS45LTIzLjFjMTcuOC0xOC41LDI0LTQ0LjEsMjQtODMuM1YwSC00Mjd2MTcwLjFMLTQyNi45LDE2OS44TC00MjYuOSwxNjkuOHoiLz4KICAgICAgPC9nPgogICAgPC9nPgogICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMTU1LjA0NTI5NiwgNTYuODM3MTA0KSI+CiAgICAgIDxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKDEuNTYyNDUzLCAxLjc5OTg0MikiPgogICAgICAgIDxwYXRoIGQ9Ik0tMzEyLDE0OGMwLDIxLDAsMzkuNSwxLjcsNTUuNGgtMzEuOGwtMi4xLTMzLjNoLTAuOGMtNi43LDExLjYtMTYuNCwyMS4zLTI4LDI3LjkgYy0xMS42LDYuNi0yNC44LDEwLTM4LjIsOS44Yy0zMS40LDAtNjktMTcuNy02OS04OVYwaDM2LjR2MTEyLjdjMCwzOC43LDExLjYsNjQuNyw0NC42LDY0LjdjMTAuMy0wLjIsMjAuNC0zLjUsMjguOS05LjQgYzguNS01LjksMTUuMS0xNC4zLDE4LjktMjMuOWMyLjItNi4xLDMuMy0xMi41LDMuMy0xOC45VjAuMmgzNi40VjE0OEgtMzEyTC0zMTIsMTQ4eiIvPgogICAgICA8L2c+CiAgICA8L2c+CiAgICA8ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgzOTAuMDEzMzIyLCA1My40Nzk2MzgpIj4KICAgICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMS43MDY0NTgsIDAuMjMxNDI1KSI+CiAgICAgICAgPHBhdGggZD0iTS00NzguNiw3MS40YzAtMjYtMC44LTQ3LTEuNy02Ni43aDMyLjdsMS43LDM0LjhoMC44YzcuMS0xMi41LDE3LjUtMjIuOCwzMC4xLTI5LjcgYzEyLjUtNywyNi43LTEwLjMsNDEtOS44YzQ4LjMsMCw4NC43LDQxLjcsODQuNywxMDMuM2MwLDczLjEtNDMuNywxMDkuMi05MSwxMDkuMmMtMTIuMSwwLjUtMjQuMi0yLjItMzUtNy44IGMtMTAuOC01LjYtMTkuOS0xMy45LTI2LjYtMjQuMmgtMC44VjI5MWgtMzZ2LTIyMEwtNDc4LjYsNzEuNEwtNDc4LjYsNzEuNHogTS00NDIuNiwxMjUuNmMwLjEsNS4xLDAuNiwxMC4xLDEuNywxNS4xIGMzLDEyLjMsOS45LDIzLjMsMTkuOCwzMS4xYzkuOSw3LjgsMjIuMSwxMi4xLDM0LjcsMTIuMWMzOC41LDAsNjAuNy0zMS45LDYwLjctNzguNWMwLTQwLjctMjEuMS03NS42LTU5LjUtNzUuNiBjLTEyLjksMC40LTI1LjMsNS4xLTM1LjMsMTMuNGMtOS45LDguMy0xNi45LDE5LjctMTkuNiwzMi40Yy0xLjUsNC45LTIuMywxMC0yLjUsMTUuMVYxMjUuNkwtNDQyLjYsMTI1LjZMLTQ0Mi42LDEyNS42eiIvPgogICAgICA8L2c+CiAgICA8L2c+CiAgICA8ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSg2MDYuNzQwNzI2LCA1Ni44MzcxMDQpIj4KICAgICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMC43NTEyMjYsIDEuOTg5Mjk5KSI+CiAgICAgICAgPHBhdGggZD0iTS00NDAuOCwwbDQzLjcsMTIwLjFjNC41LDEzLjQsOS41LDI5LjQsMTIuOCw0MS43aDAuOGMzLjctMTIuMiw3LjktMjcuNywxMi44LTQyLjQgbDM5LjctMTE5LjJoMzguNUwtMzQ2LjksMTQ1Yy0yNiw2OS43LTQzLjcsMTA1LjQtNjguNiwxMjcuMmMtMTIuNSwxMS43LTI3LjksMjAtNDQuNiwyMy45bC05LjEtMzEuMSBjMTEuNy0zLjksMjIuNS0xMC4xLDMxLjgtMTguMWMxMy4yLTExLjEsMjMuNy0yNS4yLDMwLjYtNDEuMmMxLjUtMi44LDIuNS01LjcsMi45LTguOGMtMC4zLTMuMy0xLjItNi42LTIuNS05LjdMLTQ4MC4yLDAuMSBoMzkuN0wtNDQwLjgsMEwtNDQwLjgsMHoiLz4KICAgICAgPC9nPgogICAgPC9nPgogICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoODIyLjc0ODEwNCwgMC4wMDAwMDApIj4KICAgICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMS40NjQwNTAsIDAuMzc4OTE0KSI+CiAgICAgICAgPHBhdGggZD0iTS00MTMuNywwdjU4LjNoNTJ2MjguMmgtNTJWMTk2YzAsMjUsNywzOS41LDI3LjMsMzkuNWM3LjEsMC4xLDE0LjItMC43LDIxLjEtMi41IGwxLjcsMjcuN2MtMTAuMywzLjctMjEuMyw1LjQtMzIuMiw1Yy03LjMsMC40LTE0LjYtMC43LTIxLjMtMy40Yy02LjgtMi43LTEyLjktNi44LTE3LjktMTIuMWMtMTAuMy0xMC45LTE0LjEtMjktMTQuMS01Mi45IFY4Ni41aC0zMVY1OC4zaDMxVjkuNkwtNDEzLjcsMEwtNDEzLjcsMHoiLz4KICAgICAgPC9nPgogICAgPC9nPgogICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoOTc0LjQzMzI4NiwgNTMuNDc5NjM4KSI+CiAgICAgIDxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKDAuOTkwMDM0LCAwLjYxMDMzOSkiPgogICAgICAgIDxwYXRoIGQ9Ik0tNDQ1LjgsMTEzYzAuOCw1MCwzMi4yLDcwLjYsNjguNiw3MC42YzE5LDAuNiwzNy45LTMsNTUuMy0xMC41bDYuMiwyNi40IGMtMjAuOSw4LjktNDMuNSwxMy4xLTY2LjIsMTIuNmMtNjEuNSwwLTk4LjMtNDEuMi05OC4zLTEwMi41Qy00ODAuMiw0OC4yLTQ0NC43LDAtMzg2LjUsMGM2NS4yLDAsODIuNyw1OC4zLDgyLjcsOTUuNyBjLTAuMSw1LjgtMC41LDExLjUtMS4yLDE3LjJoLTE0MC42SC00NDUuOEwtNDQ1LjgsMTEzeiBNLTMzOS4yLDg2LjZjMC40LTIzLjUtOS41LTYwLjEtNTAuNC02MC4xIGMtMzYuOCwwLTUyLjgsMzQuNC01NS43LDYwLjFILTMzOS4yTC0zMzkuMiw4Ni42TC0zMzkuMiw4Ni42eiIvPgogICAgICA8L2c+CiAgICA8L2c+CiAgICA8ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgxMjAxLjk2MTA1OCwgNTMuNDc5NjM4KSI+CiAgICAgIDxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKDEuMTc5NjQwLCAwLjcwNTA2OCkiPgogICAgICAgIDxwYXRoIGQ9Ik0tNDc4LjYsNjhjMC0yMy45LTAuNC00NC41LTEuNy02My40aDMxLjhsMS4yLDM5LjloMS43YzkuMS0yNy4zLDMxLTQ0LjUsNTUuMy00NC41IGMzLjUtMC4xLDcsMC40LDEwLjMsMS4ydjM0LjhjLTQuMS0wLjktOC4yLTEuMy0xMi40LTEuMmMtMjUuNiwwLTQzLjcsMTkuNy00OC43LDQ3LjRjLTEsNS43LTEuNiwxMS41LTEuNywxNy4ydjEwOC4zaC0zNlY2OCBMLTQ3OC42LDY4eiIvPgogICAgICA8L2c+CiAgICA8L2c+CiAgPC9nPgoKICA8ZyBjbGFzcz0ianAtaWNvbi13YXJuMCIgZmlsbD0iI0YzNzcyNiI+CiAgICA8cGF0aCBkPSJNMTM1Mi4zLDMyNi4yaDM3VjI4aC0zN1YzMjYuMnogTTE2MDQuOCwzMjYuMmMtMi41LTEzLjktMy40LTMxLjEtMy40LTQ4Ljd2LTc2IGMwLTQwLjctMTUuMS04My4xLTc3LjMtODMuMWMtMjUuNiwwLTUwLDcuMS02Ni44LDE4LjFsOC40LDI0LjRjMTQuMy05LjIsMzQtMTUuMSw1My0xNS4xYzQxLjYsMCw0Ni4yLDMwLjIsNDYuMiw0N3Y0LjIgYy03OC42LTAuNC0xMjIuMywyNi41LTEyMi4zLDc1LjZjMCwyOS40LDIxLDU4LjQsNjIuMiw1OC40YzI5LDAsNTAuOS0xNC4zLDYyLjItMzAuMmgxLjNsMi45LDI1LjZIMTYwNC44eiBNMTU2NS43LDI1Ny43IGMwLDMuOC0wLjgsOC0yLjEsMTEuOGMtNS45LDE3LjItMjIuNywzNC00OS4yLDM0Yy0xOC45LDAtMzQuOS0xMS4zLTM0LjktMzUuM2MwLTM5LjUsNDUuOC00Ni42LDg2LjItNDUuOFYyNTcuN3ogTTE2OTguNSwzMjYuMiBsMS43LTMzLjZoMS4zYzE1LjEsMjYuOSwzOC43LDM4LjIsNjguMSwzOC4yYzQ1LjQsMCw5MS4yLTM2LjEsOTEuMi0xMDguOGMwLjQtNjEuNy0zNS4zLTEwMy43LTg1LjctMTAzLjcgYy0zMi44LDAtNTYuMywxNC43LTY5LjMsMzcuNGgtMC44VjI4aC0zNi42djI0NS43YzAsMTguMS0wLjgsMzguNi0xLjcsNTIuNUgxNjk4LjV6IE0xNzA0LjgsMjA4LjJjMC01LjksMS4zLTEwLjksMi4xLTE1LjEgYzcuNi0yOC4xLDMxLjEtNDUuNCw1Ni4zLTQ1LjRjMzkuNSwwLDYwLjUsMzQuOSw2MC41LDc1LjZjMCw0Ni42LTIzLjEsNzguMS02MS44LDc4LjFjLTI2LjksMC00OC4zLTE3LjYtNTUuNS00My4zIGMtMC44LTQuMi0xLjctOC44LTEuNy0xMy40VjIwOC4yeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-kernel: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICAgIDxwYXRoIGNsYXNzPSJqcC1pY29uMiIgZmlsbD0iIzYxNjE2MSIgZD0iTTE1IDlIOXY2aDZWOXptLTIgNGgtMnYtMmgydjJ6bTgtMlY5aC0yVjdjMC0xLjEtLjktMi0yLTJoLTJWM2gtMnYyaC0yVjNIOXYySDdjLTEuMSAwLTIgLjktMiAydjJIM3YyaDJ2MkgzdjJoMnYyYzAgMS4xLjkgMiAyIDJoMnYyaDJ2LTJoMnYyaDJ2LTJoMmMxLjEgMCAyLS45IDItMnYtMmgydi0yaC0ydi0yaDJ6bS00IDZIN1Y3aDEwdjEweiIvPgo8L3N2Zz4K);
  --jp-icon-keyboard: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMjAgNUg0Yy0xLjEgMC0xLjk5LjktMS45OSAyTDIgMTdjMCAxLjEuOSAyIDIgMmgxNmMxLjEgMCAyLS45IDItMlY3YzAtMS4xLS45LTItMi0yem0tOSAzaDJ2MmgtMlY4em0wIDNoMnYyaC0ydi0yek04IDhoMnYySDhWOHptMCAzaDJ2Mkg4di0yem0tMSAySDV2LTJoMnYyem0wLTNINVY4aDJ2MnptOSA3SDh2LTJoOHYyem0wLTRoLTJ2LTJoMnYyem0wLTNoLTJWOGgydjJ6bTMgM2gtMnYtMmgydjJ6bTAtM2gtMlY4aDJ2MnoiLz4KPC9zdmc+Cg==);
  --jp-icon-launcher: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMTkgMTlINVY1aDdWM0g1YTIgMiAwIDAwLTIgMnYxNGEyIDIgMCAwMDIgMmgxNGMxLjEgMCAyLS45IDItMnYtN2gtMnY3ek0xNCAzdjJoMy41OWwtOS44MyA5LjgzIDEuNDEgMS40MUwxOSA2LjQxVjEwaDJWM2gtN3oiLz4KPC9zdmc+Cg==);
  --jp-icon-line-form: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICAgIDxwYXRoIGZpbGw9IndoaXRlIiBkPSJNNS44OCA0LjEyTDEzLjc2IDEybC03Ljg4IDcuODhMOCAyMmwxMC0xMEw4IDJ6Ii8+Cjwvc3ZnPgo=);
  --jp-icon-link: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTMuOSAxMmMwLTEuNzEgMS4zOS0zLjEgMy4xLTMuMWg0VjdIN2MtMi43NiAwLTUgMi4yNC01IDVzMi4yNCA1IDUgNWg0di0xLjlIN2MtMS43MSAwLTMuMS0xLjM5LTMuMS0zLjF6TTggMTNoOHYtMkg4djJ6bTktNmgtNHYxLjloNGMxLjcxIDAgMy4xIDEuMzkgMy4xIDMuMXMtMS4zOSAzLjEtMy4xIDMuMWgtNFYxN2g0YzIuNzYgMCA1LTIuMjQgNS01cy0yLjI0LTUtNS01eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-list: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICAgIDxwYXRoIGNsYXNzPSJqcC1pY29uMiBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiM2MTYxNjEiIGQ9Ik0xOSA1djE0SDVWNWgxNG0xLjEtMkgzLjljLS41IDAtLjkuNC0uOS45djE2LjJjMCAuNC40LjkuOS45aDE2LjJjLjQgMCAuOS0uNS45LS45VjMuOWMwLS41LS41LS45LS45LS45ek0xMSA3aDZ2MmgtNlY3em0wIDRoNnYyaC02di0yem0wIDRoNnYyaC02ek03IDdoMnYySDd6bTAgNGgydjJIN3ptMCA0aDJ2Mkg3eiIvPgo8L3N2Zz4=);
  --jp-icon-listings-info: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCA1MC45NzggNTAuOTc4IiBzdHlsZT0iZW5hYmxlLWJhY2tncm91bmQ6bmV3IDAgMCA1MC45NzggNTAuOTc4OyIgeG1sOnNwYWNlPSJwcmVzZXJ2ZSI+Cgk8Zz4KCQk8cGF0aCBzdHlsZT0iZmlsbDojMDEwMDAyOyIgZD0iTTQzLjUyLDcuNDU4QzM4LjcxMSwyLjY0OCwzMi4zMDcsMCwyNS40ODksMEMxOC42NywwLDEyLjI2NiwyLjY0OCw3LjQ1OCw3LjQ1OAoJCQljLTkuOTQzLDkuOTQxLTkuOTQzLDI2LjExOSwwLDM2LjA2MmM0LjgwOSw0LjgwOSwxMS4yMTIsNy40NTYsMTguMDMxLDcuNDU4YzAsMCwwLjAwMSwwLDAuMDAyLDAKCQkJYzYuODE2LDAsMTMuMjIxLTIuNjQ4LDE4LjAyOS03LjQ1OGM0LjgwOS00LjgwOSw3LjQ1Ny0xMS4yMTIsNy40NTctMTguMDNDNTAuOTc3LDE4LjY3LDQ4LjMyOCwxMi4yNjYsNDMuNTIsNy40NTh6CgkJCSBNNDIuMTA2LDQyLjEwNWMtNC40MzIsNC40MzEtMTAuMzMyLDYuODcyLTE2LjYxNSw2Ljg3MmgtMC4wMDJjLTYuMjg1LTAuMDAxLTEyLjE4Ny0yLjQ0MS0xNi42MTctNi44NzIKCQkJYy05LjE2Mi05LjE2My05LjE2Mi0yNC4wNzEsMC0zMy4yMzNDMTMuMzAzLDQuNDQsMTkuMjA0LDIsMjUuNDg5LDJjNi4yODQsMCwxMi4xODYsMi40NCwxNi42MTcsNi44NzIKCQkJYzQuNDMxLDQuNDMxLDYuODcxLDEwLjMzMiw2Ljg3MSwxNi42MTdDNDguOTc3LDMxLjc3Miw0Ni41MzYsMzcuNjc1LDQyLjEwNiw0Mi4xMDV6Ii8+CgkJPHBhdGggc3R5bGU9ImZpbGw6IzAxMDAwMjsiIGQ9Ik0yMy41NzgsMzIuMjE4Yy0wLjAyMy0xLjczNCwwLjE0My0zLjA1OSwwLjQ5Ni0zLjk3MmMwLjM1My0wLjkxMywxLjExLTEuOTk3LDIuMjcyLTMuMjUzCgkJCWMwLjQ2OC0wLjUzNiwwLjkyMy0xLjA2MiwxLjM2Ny0xLjU3NWMwLjYyNi0wLjc1MywxLjEwNC0xLjQ3OCwxLjQzNi0yLjE3NWMwLjMzMS0wLjcwNywwLjQ5NS0xLjU0MSwwLjQ5NS0yLjUKCQkJYzAtMS4wOTYtMC4yNi0yLjA4OC0wLjc3OS0yLjk3OWMtMC41NjUtMC44NzktMS41MDEtMS4zMzYtMi44MDYtMS4zNjljLTEuODAyLDAuMDU3LTIuOTg1LDAuNjY3LTMuNTUsMS44MzIKCQkJYy0wLjMwMSwwLjUzNS0wLjUwMywxLjE0MS0wLjYwNywxLjgxNGMtMC4xMzksMC43MDctMC4yMDcsMS40MzItMC4yMDcsMi4xNzRoLTIuOTM3Yy0wLjA5MS0yLjIwOCwwLjQwNy00LjExNCwxLjQ5My01LjcxOQoJCQljMS4wNjItMS42NCwyLjg1NS0yLjQ4MSw1LjM3OC0yLjUyN2MyLjE2LDAuMDIzLDMuODc0LDAuNjA4LDUuMTQxLDEuNzU4YzEuMjc4LDEuMTYsMS45MjksMi43NjQsMS45NSw0LjgxMQoJCQljMCwxLjE0Mi0wLjEzNywyLjExMS0wLjQxLDIuOTExYy0wLjMwOSwwLjg0NS0wLjczMSwxLjU5My0xLjI2OCwyLjI0M2MtMC40OTIsMC42NS0xLjA2OCwxLjMxOC0xLjczLDIuMDAyCgkJCWMtMC42NSwwLjY5Ny0xLjMxMywxLjQ3OS0xLjk4NywyLjM0NmMtMC4yMzksMC4zNzctMC40MjksMC43NzctMC41NjUsMS4xOTljLTAuMTYsMC45NTktMC4yMTcsMS45NTEtMC4xNzEsMi45NzkKCQkJQzI2LjU4OSwzMi4yMTgsMjMuNTc4LDMyLjIxOCwyMy41NzgsMzIuMjE4eiBNMjMuNTc4LDM4LjIydi0zLjQ4NGgzLjA3NnYzLjQ4NEgyMy41Nzh6Ii8+Cgk8L2c+Cjwvc3ZnPgo=);
  --jp-icon-markdown: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8cGF0aCBjbGFzcz0ianAtaWNvbi1jb250cmFzdDAganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjN0IxRkEyIiBkPSJNNSAxNC45aDEybC02LjEgNnptOS40LTYuOGMwLTEuMy0uMS0yLjktLjEtNC41LS40IDEuNC0uOSAyLjktMS4zIDQuM2wtMS4zIDQuM2gtMkw4LjUgNy45Yy0uNC0xLjMtLjctMi45LTEtNC4zLS4xIDEuNi0uMSAzLjItLjIgNC42TDcgMTIuNEg0LjhsLjctMTFoMy4zTDEwIDVjLjQgMS4yLjcgMi43IDEgMy45LjMtMS4yLjctMi42IDEtMy45bDEuMi0zLjdoMy4zbC42IDExaC0yLjRsLS4zLTQuMnoiLz4KPC9zdmc+Cg==);
  --jp-icon-new-folder: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTIwIDZoLThsLTItMkg0Yy0xLjExIDAtMS45OS44OS0xLjk5IDJMMiAxOGMwIDEuMTEuODkgMiAyIDJoMTZjMS4xMSAwIDItLjg5IDItMlY4YzAtMS4xMS0uODktMi0yLTJ6bS0xIDhoLTN2M2gtMnYtM2gtM3YtMmgzVjloMnYzaDN2MnoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-not-trusted: url(data:image/svg+xml;base64,PHN2ZyBmaWxsPSJub25lIiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI1IDI1Ij4KICAgIDxwYXRoIGNsYXNzPSJqcC1pY29uMiIgc3Ryb2tlPSIjMzMzMzMzIiBzdHJva2Utd2lkdGg9IjIiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDMgMykiIGQ9Ik0xLjg2MDk0IDExLjQ0MDlDMC44MjY0NDggOC43NzAyNyAwLjg2Mzc3OSA2LjA1NzY0IDEuMjQ5MDcgNC4xOTkzMkMyLjQ4MjA2IDMuOTMzNDcgNC4wODA2OCAzLjQwMzQ3IDUuNjAxMDIgMi44NDQ5QzcuMjM1NDkgMi4yNDQ0IDguODU2NjYgMS41ODE1IDkuOTg3NiAxLjA5NTM5QzExLjA1OTcgMS41ODM0MSAxMi42MDk0IDIuMjQ0NCAxNC4yMTggMi44NDMzOUMxNS43NTAzIDMuNDEzOTQgMTcuMzk5NSAzLjk1MjU4IDE4Ljc1MzkgNC4yMTM4NUMxOS4xMzY0IDYuMDcxNzcgMTkuMTcwOSA4Ljc3NzIyIDE4LjEzOSAxMS40NDA5QzE3LjAzMDMgMTQuMzAzMiAxNC42NjY4IDE3LjE4NDQgOS45OTk5OSAxOC45MzU0QzUuMzMzMTkgMTcuMTg0NCAyLjk2OTY4IDE0LjMwMzIgMS44NjA5NCAxMS40NDA5WiIvPgogICAgPHBhdGggY2xhc3M9ImpwLWljb24yIiBzdHJva2U9IiMzMzMzMzMiIHN0cm9rZS13aWR0aD0iMiIgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoOS4zMTU5MiA5LjMyMDMxKSIgZD0iTTcuMzY4NDIgMEwwIDcuMzY0NzkiLz4KICAgIDxwYXRoIGNsYXNzPSJqcC1pY29uMiIgc3Ryb2tlPSIjMzMzMzMzIiBzdHJva2Utd2lkdGg9IjIiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDkuMzE1OTIgMTYuNjgzNikgc2NhbGUoMSAtMSkiIGQ9Ik03LjM2ODQyIDBMMCA3LjM2NDc5Ii8+Cjwvc3ZnPgo=);
  --jp-icon-notebook: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8ZyBjbGFzcz0ianAtaWNvbi13YXJuMCBqcC1pY29uLXNlbGVjdGFibGUiIGZpbGw9IiNFRjZDMDAiPgogICAgPHBhdGggZD0iTTE4LjcgMy4zdjE1LjRIMy4zVjMuM2gxNS40bTEuNS0xLjVIMS44djE4LjNoMTguM2wuMS0xOC4zeiIvPgogICAgPHBhdGggZD0iTTE2LjUgMTYuNWwtNS40LTQuMy01LjYgNC4zdi0xMWgxMXoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-numbering: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjIiIGhlaWdodD0iMjIiIHZpZXdCb3g9IjAgMCAyOCAyOCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CgkJPHBhdGggZD0iTTQgMTlINlYxOS41SDVWMjAuNUg2VjIxSDRWMjJIN1YxOEg0VjE5Wk01IDEwSDZWNkg0VjdINVYxMFpNNCAxM0g1LjhMNCAxNS4xVjE2SDdWMTVINS4yTDcgMTIuOVYxMkg0VjEzWk05IDdWOUgyM1Y3SDlaTTkgMjFIMjNWMTlIOVYyMVpNOSAxNUgyM1YxM0g5VjE1WiIvPgoJPC9nPgo8L3N2Zz4K);
  --jp-icon-offline-bolt: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCIgd2lkdGg9IjE2Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTEyIDIuMDJjLTUuNTEgMC05Ljk4IDQuNDctOS45OCA5Ljk4czQuNDcgOS45OCA5Ljk4IDkuOTggOS45OC00LjQ3IDkuOTgtOS45OFMxNy41MSAyLjAyIDEyIDIuMDJ6TTExLjQ4IDIwdi02LjI2SDhMMTMgNHY2LjI2aDMuMzVMMTEuNDggMjB6Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-palette: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTE4IDEzVjIwSDRWNkg5LjAyQzkuMDcgNS4yOSA5LjI0IDQuNjIgOS41IDRINEMyLjkgNCAyIDQuOSAyIDZWMjBDMiAyMS4xIDIuOSAyMiA0IDIySDE4QzE5LjEgMjIgMjAgMjEuMSAyMCAyMFYxNUwxOCAxM1pNMTkuMyA4Ljg5QzE5Ljc0IDguMTkgMjAgNy4zOCAyMCA2LjVDMjAgNC4wMSAxNy45OSAyIDE1LjUgMkMxMy4wMSAyIDExIDQuMDEgMTEgNi41QzExIDguOTkgMTMuMDEgMTEgMTUuNDkgMTFDMTYuMzcgMTEgMTcuMTkgMTAuNzQgMTcuODggMTAuM0wyMSAxMy40MkwyMi40MiAxMkwxOS4zIDguODlaTTE1LjUgOUMxNC4xMiA5IDEzIDcuODggMTMgNi41QzEzIDUuMTIgMTQuMTIgNCAxNS41IDRDMTYuODggNCAxOCA1LjEyIDE4IDYuNUMxOCA3Ljg4IDE2Ljg4IDkgMTUuNSA5WiIvPgogICAgPHBhdGggZmlsbC1ydWxlPSJldmVub2RkIiBjbGlwLXJ1bGU9ImV2ZW5vZGQiIGQ9Ik00IDZIOS4wMTg5NEM5LjAwNjM5IDYuMTY1MDIgOSA2LjMzMTc2IDkgNi41QzkgOC44MTU3NyAxMC4yMTEgMTAuODQ4NyAxMi4wMzQzIDEySDlWMTRIMTZWMTIuOTgxMUMxNi41NzAzIDEyLjkzNzcgMTcuMTIgMTIuODIwNyAxNy42Mzk2IDEyLjYzOTZMMTggMTNWMjBINFY2Wk04IDhINlYxMEg4VjhaTTYgMTJIOFYxNEg2VjEyWk04IDE2SDZWMThIOFYxNlpNOSAxNkgxNlYxOEg5VjE2WiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-paste: url(data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTE5IDJoLTQuMThDMTQuNC44NCAxMy4zIDAgMTIgMGMtMS4zIDAtMi40Ljg0LTIuODIgMkg1Yy0xLjEgMC0yIC45LTIgMnYxNmMwIDEuMS45IDIgMiAyaDE0YzEuMSAwIDItLjkgMi0yVjRjMC0xLjEtLjktMi0yLTJ6bS03IDBjLjU1IDAgMSAuNDUgMSAxcy0uNDUgMS0xIDEtMS0uNDUtMS0xIC40NS0xIDEtMXptNyAxOEg1VjRoMnYzaDEwVjRoMnYxNnoiLz4KICAgIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-pdf: url(data:image/svg+xml;base64,PHN2ZwogICB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyMiAyMiIgd2lkdGg9IjE2Ij4KICAgIDxwYXRoIHRyYW5zZm9ybT0icm90YXRlKDQ1KSIgY2xhc3M9ImpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iI0ZGMkEyQSIKICAgICAgIGQ9Im0gMjIuMzQ0MzY5LC0zLjAxNjM2NDIgaCA1LjYzODYwNCB2IDEuNTc5MjQzMyBoIC0zLjU0OTIyNyB2IDEuNTA4NjkyOTkgaCAzLjMzNzU3NiBWIDEuNjUwODE1NCBoIC0zLjMzNzU3NiB2IDMuNDM1MjYxMyBoIC0yLjA4OTM3NyB6IG0gLTcuMTM2NDQ0LDEuNTc5MjQzMyB2IDQuOTQzOTU0MyBoIDAuNzQ4OTIgcSAxLjI4MDc2MSwwIDEuOTUzNzAzLC0wLjYzNDk1MzUgMC42NzgzNjksLTAuNjM0OTUzNSAwLjY3ODM2OSwtMS44NDUxNjQxIDAsLTEuMjA0NzgzNTUgLTAuNjcyOTQyLC0xLjgzNDMxMDExIC0wLjY3Mjk0MiwtMC42Mjk1MjY1OSAtMS45NTkxMywtMC42Mjk1MjY1OSB6IG0gLTIuMDg5Mzc3LC0xLjU3OTI0MzMgaCAyLjIwMzM0MyBxIDEuODQ1MTY0LDAgMi43NDYwMzksMC4yNjU5MjA3IDAuOTA2MzAxLDAuMjYwNDkzNyAxLjU1MjEwOCwwLjg5MDAyMDMgMC41Njk4MywwLjU0ODEyMjMgMC44NDY2MDUsMS4yNjQ0ODAwNiAwLjI3Njc3NCwwLjcxNjM1NzgxIDAuMjc2Nzc0LDEuNjIyNjU4OTQgMCwwLjkxNzE1NTEgLTAuMjc2Nzc0LDEuNjM4OTM5OSAtMC4yNzY3NzUsMC43MTYzNTc4IC0wLjg0NjYwNSwxLjI2NDQ4IC0wLjY1MTIzNCwwLjYyOTUyNjYgLTEuNTYyOTYyLDAuODk1NDQ3MyAtMC45MTE3MjgsMC4yNjA0OTM3IC0yLjczNTE4NSwwLjI2MDQ5MzcgaCAtMi4yMDMzNDMgeiBtIC04LjE0NTg1NjUsMCBoIDMuNDY3ODIzIHEgMS41NDY2ODE2LDAgMi4zNzE1Nzg1LDAuNjg5MjIzIDAuODMwMzI0LDAuNjgzNzk2MSAwLjgzMDMyNCwxLjk1MzcwMzE0IDAsMS4yNzUzMzM5NyAtMC44MzAzMjQsMS45NjQ1NTcwNiBRIDkuOTg3MTk2MSwyLjI3NDkxNSA4LjQ0MDUxNDUsMi4yNzQ5MTUgSCA3LjA2MjA2ODQgViA1LjA4NjA3NjcgSCA0Ljk3MjY5MTUgWiBtIDIuMDg5Mzc2OSwxLjUxNDExOTkgdiAyLjI2MzAzOTQzIGggMS4xNTU5NDEgcSAwLjYwNzgxODgsMCAwLjkzODg2MjksLTAuMjkzMDU1NDcgMC4zMzEwNDQxLC0wLjI5ODQ4MjQxIDAuMzMxMDQ0MSwtMC44NDExNzc3MiAwLC0wLjU0MjY5NTMxIC0wLjMzMTA0NDEsLTAuODM1NzUwNzQgLTAuMzMxMDQ0MSwtMC4yOTMwNTU1IC0wLjkzODg2MjksLTAuMjkzMDU1NSB6IgovPgo8L3N2Zz4K);
  --jp-icon-python: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8ZyBjbGFzcz0ianAtaWNvbi1icmFuZDAganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjMEQ0N0ExIj4KICAgIDxwYXRoIGQ9Ik0xMS4xIDYuOVY1LjhINi45YzAtLjUgMC0xLjMuMi0xLjYuNC0uNy44LTEuMSAxLjctMS40IDEuNy0uMyAyLjUtLjMgMy45LS4xIDEgLjEgMS45LjkgMS45IDEuOXY0LjJjMCAuNS0uOSAxLjYtMiAxLjZIOC44Yy0xLjUgMC0yLjQgMS40LTIuNCAyLjh2Mi4ySDQuN0MzLjUgMTUuMSAzIDE0IDMgMTMuMVY5Yy0uMS0xIC42LTIgMS44LTIgMS41LS4xIDYuMy0uMSA2LjMtLjF6Ii8+CiAgICA8cGF0aCBkPSJNMTAuOSAxNS4xdjEuMWg0LjJjMCAuNSAwIDEuMy0uMiAxLjYtLjQuNy0uOCAxLjEtMS43IDEuNC0xLjcuMy0yLjUuMy0zLjkuMS0xLS4xLTEuOS0uOS0xLjktMS45di00LjJjMC0uNS45LTEuNiAyLTEuNmgzLjhjMS41IDAgMi40LTEuNCAyLjQtMi44VjYuNmgxLjdDMTguNSA2LjkgMTkgOCAxOSA4LjlWMTNjMCAxLS43IDIuMS0xLjkgMi4xaC02LjJ6Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-r-kernel: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8cGF0aCBjbGFzcz0ianAtaWNvbi1jb250cmFzdDMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjMjE5NkYzIiBkPSJNNC40IDIuNWMxLjItLjEgMi45LS4zIDQuOS0uMyAyLjUgMCA0LjEuNCA1LjIgMS4zIDEgLjcgMS41IDEuOSAxLjUgMy41IDAgMi0xLjQgMy41LTIuOSA0LjEgMS4yLjQgMS43IDEuNiAyLjIgMyAuNiAxLjkgMSAzLjkgMS4zIDQuNmgtMy44Yy0uMy0uNC0uOC0xLjctMS4yLTMuN3MtMS4yLTIuNi0yLjYtMi42aC0uOXY2LjRINC40VjIuNXptMy43IDYuOWgxLjRjMS45IDAgMi45LS45IDIuOS0yLjNzLTEtMi4zLTIuOC0yLjNjLS43IDAtMS4zIDAtMS42LjJ2NC41aC4xdi0uMXoiLz4KPC9zdmc+Cg==);
  --jp-icon-react: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMTUwIDE1MCA1NDEuOSAyOTUuMyI+CiAgPGcgY2xhc3M9ImpwLWljb24tYnJhbmQyIGpwLWljb24tc2VsZWN0YWJsZSIgZmlsbD0iIzYxREFGQiI+CiAgICA8cGF0aCBkPSJNNjY2LjMgMjk2LjVjMC0zMi41LTQwLjctNjMuMy0xMDMuMS04Mi40IDE0LjQtNjMuNiA4LTExNC4yLTIwLjItMTMwLjQtNi41LTMuOC0xNC4xLTUuNi0yMi40LTUuNnYyMi4zYzQuNiAwIDguMy45IDExLjQgMi42IDEzLjYgNy44IDE5LjUgMzcuNSAxNC45IDc1LjctMS4xIDkuNC0yLjkgMTkuMy01LjEgMjkuNC0xOS42LTQuOC00MS04LjUtNjMuNS0xMC45LTEzLjUtMTguNS0yNy41LTM1LjMtNDEuNi01MCAzMi42LTMwLjMgNjMuMi00Ni45IDg0LTQ2LjlWNzhjLTI3LjUgMC02My41IDE5LjYtOTkuOSA1My42LTM2LjQtMzMuOC03Mi40LTUzLjItOTkuOS01My4ydjIyLjNjMjAuNyAwIDUxLjQgMTYuNSA4NCA0Ni42LTE0IDE0LjctMjggMzEuNC00MS4zIDQ5LjktMjIuNiAyLjQtNDQgNi4xLTYzLjYgMTEtMi4zLTEwLTQtMTkuNy01LjItMjktNC43LTM4LjIgMS4xLTY3LjkgMTQuNi03NS44IDMtMS44IDYuOS0yLjYgMTEuNS0yLjZWNzguNWMtOC40IDAtMTYgMS44LTIyLjYgNS42LTI4LjEgMTYuMi0zNC40IDY2LjctMTkuOSAxMzAuMS02Mi4yIDE5LjItMTAyLjcgNDkuOS0xMDIuNyA4Mi4zIDAgMzIuNSA0MC43IDYzLjMgMTAzLjEgODIuNC0xNC40IDYzLjYtOCAxMTQuMiAyMC4yIDEzMC40IDYuNSAzLjggMTQuMSA1LjYgMjIuNSA1LjYgMjcuNSAwIDYzLjUtMTkuNiA5OS45LTUzLjYgMzYuNCAzMy44IDcyLjQgNTMuMiA5OS45IDUzLjIgOC40IDAgMTYtMS44IDIyLjYtNS42IDI4LjEtMTYuMiAzNC40LTY2LjcgMTkuOS0xMzAuMSA2Mi0xOS4xIDEwMi41LTQ5LjkgMTAyLjUtODIuM3ptLTEzMC4yLTY2LjdjLTMuNyAxMi45LTguMyAyNi4yLTEzLjUgMzkuNS00LjEtOC04LjQtMTYtMTMuMS0yNC00LjYtOC05LjUtMTUuOC0xNC40LTIzLjQgMTQuMiAyLjEgMjcuOSA0LjcgNDEgNy45em0tNDUuOCAxMDYuNWMtNy44IDEzLjUtMTUuOCAyNi4zLTI0LjEgMzguMi0xNC45IDEuMy0zMCAyLTQ1LjIgMi0xNS4xIDAtMzAuMi0uNy00NS0xLjktOC4zLTExLjktMTYuNC0yNC42LTI0LjItMzgtNy42LTEzLjEtMTQuNS0yNi40LTIwLjgtMzkuOCA2LjItMTMuNCAxMy4yLTI2LjggMjAuNy0zOS45IDcuOC0xMy41IDE1LjgtMjYuMyAyNC4xLTM4LjIgMTQuOS0xLjMgMzAtMiA0NS4yLTIgMTUuMSAwIDMwLjIuNyA0NSAxLjkgOC4zIDExLjkgMTYuNCAyNC42IDI0LjIgMzggNy42IDEzLjEgMTQuNSAyNi40IDIwLjggMzkuOC02LjMgMTMuNC0xMy4yIDI2LjgtMjAuNyAzOS45em0zMi4zLTEzYzUuNCAxMy40IDEwIDI2LjggMTMuOCAzOS44LTEzLjEgMy4yLTI2LjkgNS45LTQxLjIgOCA0LjktNy43IDkuOC0xNS42IDE0LjQtMjMuNyA0LjYtOCA4LjktMTYuMSAxMy0yNC4xek00MjEuMiA0MzBjLTkuMy05LjYtMTguNi0yMC4zLTI3LjgtMzIgOSAuNCAxOC4yLjcgMjcuNS43IDkuNCAwIDE4LjctLjIgMjcuOC0uNy05IDExLjctMTguMyAyMi40LTI3LjUgMzJ6bS03NC40LTU4LjljLTE0LjItMi4xLTI3LjktNC43LTQxLTcuOSAzLjctMTIuOSA4LjMtMjYuMiAxMy41LTM5LjUgNC4xIDggOC40IDE2IDEzLjEgMjQgNC43IDggOS41IDE1LjggMTQuNCAyMy40ek00MjAuNyAxNjNjOS4zIDkuNiAxOC42IDIwLjMgMjcuOCAzMi05LS40LTE4LjItLjctMjcuNS0uNy05LjQgMC0xOC43LjItMjcuOC43IDktMTEuNyAxOC4zLTIyLjQgMjcuNS0zMnptLTc0IDU4LjljLTQuOSA3LjctOS44IDE1LjYtMTQuNCAyMy43LTQuNiA4LTguOSAxNi0xMyAyNC01LjQtMTMuNC0xMC0yNi44LTEzLjgtMzkuOCAxMy4xLTMuMSAyNi45LTUuOCA0MS4yLTcuOXptLTkwLjUgMTI1LjJjLTM1LjQtMTUuMS01OC4zLTM0LjktNTguMy01MC42IDAtMTUuNyAyMi45LTM1LjYgNTguMy01MC42IDguNi0zLjcgMTgtNyAyNy43LTEwLjEgNS43IDE5LjYgMTMuMiA0MCAyMi41IDYwLjktOS4yIDIwLjgtMTYuNiA0MS4xLTIyLjIgNjAuNi05LjktMy4xLTE5LjMtNi41LTI4LTEwLjJ6TTMxMCA0OTBjLTEzLjYtNy44LTE5LjUtMzcuNS0xNC45LTc1LjcgMS4xLTkuNCAyLjktMTkuMyA1LjEtMjkuNCAxOS42IDQuOCA0MSA4LjUgNjMuNSAxMC45IDEzLjUgMTguNSAyNy41IDM1LjMgNDEuNiA1MC0zMi42IDMwLjMtNjMuMiA0Ni45LTg0IDQ2LjktNC41LS4xLTguMy0xLTExLjMtMi43em0yMzcuMi03Ni4yYzQuNyAzOC4yLTEuMSA2Ny45LTE0LjYgNzUuOC0zIDEuOC02LjkgMi42LTExLjUgMi42LTIwLjcgMC01MS40LTE2LjUtODQtNDYuNiAxNC0xNC43IDI4LTMxLjQgNDEuMy00OS45IDIyLjYtMi40IDQ0LTYuMSA2My42LTExIDIuMyAxMC4xIDQuMSAxOS44IDUuMiAyOS4xem0zOC41LTY2LjdjLTguNiAzLjctMTggNy0yNy43IDEwLjEtNS43LTE5LjYtMTMuMi00MC0yMi41LTYwLjkgOS4yLTIwLjggMTYuNi00MS4xIDIyLjItNjAuNiA5LjkgMy4xIDE5LjMgNi41IDI4LjEgMTAuMiAzNS40IDE1LjEgNTguMyAzNC45IDU4LjMgNTAuNi0uMSAxNS43LTIzIDM1LjYtNTguNCA1MC42ek0zMjAuOCA3OC40eiIvPgogICAgPGNpcmNsZSBjeD0iNDIwLjkiIGN5PSIyOTYuNSIgcj0iNDUuNyIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-redo: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIGhlaWdodD0iMjQiIHZpZXdCb3g9IjAgMCAyNCAyNCIgd2lkdGg9IjE2Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgICA8cGF0aCBkPSJNMCAwaDI0djI0SDB6IiBmaWxsPSJub25lIi8+PHBhdGggZD0iTTE4LjQgMTAuNkMxNi41NSA4Ljk5IDE0LjE1IDggMTEuNSA4Yy00LjY1IDAtOC41OCAzLjAzLTkuOTYgNy4yMkwzLjkgMTZjMS4wNS0zLjE5IDQuMDUtNS41IDcuNi01LjUgMS45NSAwIDMuNzMuNzIgNS4xMiAxLjg4TDEzIDE2aDlWN2wtMy42IDMuNnoiLz4KICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-refresh: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDE4IDE4Ij4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTkgMTMuNWMtMi40OSAwLTQuNS0yLjAxLTQuNS00LjVTNi41MSA0LjUgOSA0LjVjMS4yNCAwIDIuMzYuNTIgMy4xNyAxLjMzTDEwIDhoNVYzbC0xLjc2IDEuNzZDMTIuMTUgMy42OCAxMC42NiAzIDkgMyA1LjY5IDMgMy4wMSA1LjY5IDMuMDEgOVM1LjY5IDE1IDkgMTVjMi45NyAwIDUuNDMtMi4xNiA1LjktNWgtMS41MmMtLjQ2IDItMi4yNCAzLjUtNC4zOCAzLjV6Ii8+CiAgICA8L2c+Cjwvc3ZnPgo=);
  --jp-icon-regex: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIwIDIwIj4KICA8ZyBjbGFzcz0ianAtaWNvbjIiIGZpbGw9IiM0MTQxNDEiPgogICAgPHJlY3QgeD0iMiIgeT0iMiIgd2lkdGg9IjE2IiBoZWlnaHQ9IjE2Ii8+CiAgPC9nPgoKICA8ZyBjbGFzcz0ianAtaWNvbi1hY2NlbnQyIiBmaWxsPSIjRkZGIj4KICAgIDxjaXJjbGUgY2xhc3M9InN0MiIgY3g9IjUuNSIgY3k9IjE0LjUiIHI9IjEuNSIvPgogICAgPHJlY3QgeD0iMTIiIHk9IjQiIGNsYXNzPSJzdDIiIHdpZHRoPSIxIiBoZWlnaHQ9IjgiLz4KICAgIDxyZWN0IHg9IjguNSIgeT0iNy41IiB0cmFuc2Zvcm09Im1hdHJpeCgwLjg2NiAtMC41IDAuNSAwLjg2NiAtMi4zMjU1IDcuMzIxOSkiIGNsYXNzPSJzdDIiIHdpZHRoPSI4IiBoZWlnaHQ9IjEiLz4KICAgIDxyZWN0IHg9IjEyIiB5PSI0IiB0cmFuc2Zvcm09Im1hdHJpeCgwLjUgLTAuODY2IDAuODY2IDAuNSAtMC42Nzc5IDE0LjgyNTIpIiBjbGFzcz0ic3QyIiB3aWR0aD0iMSIgaGVpZ2h0PSI4Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-run: url(data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTggNXYxNGwxMS03eiIvPgogICAgPC9nPgo8L3N2Zz4K);
  --jp-icon-running: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDUxMiA1MTIiPgogIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICA8cGF0aCBkPSJNMjU2IDhDMTE5IDggOCAxMTkgOCAyNTZzMTExIDI0OCAyNDggMjQ4IDI0OC0xMTEgMjQ4LTI0OFMzOTMgOCAyNTYgOHptOTYgMzI4YzAgOC44LTcuMiAxNi0xNiAxNkgxNzZjLTguOCAwLTE2LTcuMi0xNi0xNlYxNzZjMC04LjggNy4yLTE2IDE2LTE2aDE2MGM4LjggMCAxNiA3LjIgMTYgMTZ2MTYweiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-save: url(data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTE3IDNINWMtMS4xMSAwLTIgLjktMiAydjE0YzAgMS4xLjg5IDIgMiAyaDE0YzEuMSAwIDItLjkgMi0yVjdsLTQtNHptLTUgMTZjLTEuNjYgMC0zLTEuMzQtMy0zczEuMzQtMyAzLTMgMyAxLjM0IDMgMy0xLjM0IDMtMyAzem0zLTEwSDVWNWgxMHY0eiIvPgogICAgPC9nPgo8L3N2Zz4K);
  --jp-icon-search: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMTggMTgiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTEyLjEsMTAuOWgtMC43bC0wLjItMC4yYzAuOC0wLjksMS4zLTIuMiwxLjMtMy41YzAtMy0yLjQtNS40LTUuNC01LjRTMS44LDQuMiwxLjgsNy4xczIuNCw1LjQsNS40LDUuNCBjMS4zLDAsMi41LTAuNSwzLjUtMS4zbDAuMiwwLjJ2MC43bDQuMSw0LjFsMS4yLTEuMkwxMi4xLDEwLjl6IE03LjEsMTAuOWMtMi4xLDAtMy43LTEuNy0zLjctMy43czEuNy0zLjcsMy43LTMuN3MzLjcsMS43LDMuNywzLjcgUzkuMiwxMC45LDcuMSwxMC45eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-settings: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMTkuNDMgMTIuOThjLjA0LS4zMi4wNy0uNjQuMDctLjk4cy0uMDMtLjY2LS4wNy0uOThsMi4xMS0xLjY1Yy4xOS0uMTUuMjQtLjQyLjEyLS42NGwtMi0zLjQ2Yy0uMTItLjIyLS4zOS0uMy0uNjEtLjIybC0yLjQ5IDFjLS41Mi0uNC0xLjA4LS43My0xLjY5LS45OGwtLjM4LTIuNjVBLjQ4OC40ODggMCAwMDE0IDJoLTRjLS4yNSAwLS40Ni4xOC0uNDkuNDJsLS4zOCAyLjY1Yy0uNjEuMjUtMS4xNy41OS0xLjY5Ljk4bC0yLjQ5LTFjLS4yMy0uMDktLjQ5IDAtLjYxLjIybC0yIDMuNDZjLS4xMy4yMi0uMDcuNDkuMTIuNjRsMi4xMSAxLjY1Yy0uMDQuMzItLjA3LjY1LS4wNy45OHMuMDMuNjYuMDcuOThsLTIuMTEgMS42NWMtLjE5LjE1LS4yNC40Mi0uMTIuNjRsMiAzLjQ2Yy4xMi4yMi4zOS4zLjYxLjIybDIuNDktMWMuNTIuNCAxLjA4LjczIDEuNjkuOThsLjM4IDIuNjVjLjAzLjI0LjI0LjQyLjQ5LjQyaDRjLjI1IDAgLjQ2LS4xOC40OS0uNDJsLjM4LTIuNjVjLjYxLS4yNSAxLjE3LS41OSAxLjY5LS45OGwyLjQ5IDFjLjIzLjA5LjQ5IDAgLjYxLS4yMmwyLTMuNDZjLjEyLS4yMi4wNy0uNDktLjEyLS42NGwtMi4xMS0xLjY1ek0xMiAxNS41Yy0xLjkzIDAtMy41LTEuNTctMy41LTMuNXMxLjU3LTMuNSAzLjUtMy41IDMuNSAxLjU3IDMuNSAzLjUtMS41NyAzLjUtMy41IDMuNXoiLz4KPC9zdmc+Cg==);
  --jp-icon-spreadsheet: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8cGF0aCBjbGFzcz0ianAtaWNvbi1jb250cmFzdDEganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNENBRjUwIiBkPSJNMi4yIDIuMnYxNy42aDE3LjZWMi4ySDIuMnptMTUuNCA3LjdoLTUuNVY0LjRoNS41djUuNXpNOS45IDQuNHY1LjVINC40VjQuNGg1LjV6bS01LjUgNy43aDUuNXY1LjVINC40di01LjV6bTcuNyA1LjV2LTUuNWg1LjV2NS41aC01LjV6Ii8+Cjwvc3ZnPgo=);
  --jp-icon-stop: url(data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTAgMGgyNHYyNEgweiIgZmlsbD0ibm9uZSIvPgogICAgICAgIDxwYXRoIGQ9Ik02IDZoMTJ2MTJINnoiLz4KICAgIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-tab: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTIxIDNIM2MtMS4xIDAtMiAuOS0yIDJ2MTRjMCAxLjEuOSAyIDIgMmgxOGMxLjEgMCAyLS45IDItMlY1YzAtMS4xLS45LTItMi0yem0wIDE2SDNWNWgxMHY0aDh2MTB6Ii8+CiAgPC9nPgo8L3N2Zz4K);
  --jp-icon-table-rows: url(data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTAgMGgyNHYyNEgweiIgZmlsbD0ibm9uZSIvPgogICAgICAgIDxwYXRoIGQ9Ik0yMSw4SDNWNGgxOFY4eiBNMjEsMTBIM3Y0aDE4VjEweiBNMjEsMTZIM3Y0aDE4VjE2eiIvPgogICAgPC9nPgo8L3N2Zz4=);
  --jp-icon-tag: url(data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjgiIGhlaWdodD0iMjgiIHZpZXdCb3g9IjAgMCA0MyAyOCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KCTxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CgkJPHBhdGggZD0iTTI4LjgzMzIgMTIuMzM0TDMyLjk5OTggMTYuNTAwN0wzNy4xNjY1IDEyLjMzNEgyOC44MzMyWiIvPgoJCTxwYXRoIGQ9Ik0xNi4yMDk1IDIxLjYxMDRDMTUuNjg3MyAyMi4xMjk5IDE0Ljg0NDMgMjIuMTI5OSAxNC4zMjQ4IDIxLjYxMDRMNi45ODI5IDE0LjcyNDVDNi41NzI0IDE0LjMzOTQgNi4wODMxMyAxMy42MDk4IDYuMDQ3ODYgMTMuMDQ4MkM1Ljk1MzQ3IDExLjUyODggNi4wMjAwMiA4LjYxOTQ0IDYuMDY2MjEgNy4wNzY5NUM2LjA4MjgxIDYuNTE0NzcgNi41NTU0OCA2LjA0MzQ3IDcuMTE4MDQgNi4wMzA1NUM5LjA4ODYzIDUuOTg0NzMgMTMuMjYzOCA1LjkzNTc5IDEzLjY1MTggNi4zMjQyNUwyMS43MzY5IDEzLjYzOUMyMi4yNTYgMTQuMTU4NSAyMS43ODUxIDE1LjQ3MjQgMjEuMjYyIDE1Ljk5NDZMMTYuMjA5NSAyMS42MTA0Wk05Ljc3NTg1IDguMjY1QzkuMzM1NTEgNy44MjU2NiA4LjYyMzUxIDcuODI1NjYgOC4xODI4IDguMjY1QzcuNzQzNDYgOC43MDU3MSA3Ljc0MzQ2IDkuNDE3MzMgOC4xODI4IDkuODU2NjdDOC42MjM4MiAxMC4yOTY0IDkuMzM1ODIgMTAuMjk2NCA5Ljc3NTg1IDkuODU2NjdDMTAuMjE1NiA5LjQxNzMzIDEwLjIxNTYgOC43MDUzMyA5Ljc3NTg1IDguMjY1WiIvPgoJPC9nPgo8L3N2Zz4K);
  --jp-icon-terminal: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0IiA+CiAgICA8cmVjdCBjbGFzcz0ianAtaWNvbjIganAtaWNvbi1zZWxlY3RhYmxlIiB3aWR0aD0iMjAiIGhlaWdodD0iMjAiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDIgMikiIGZpbGw9IiMzMzMzMzMiLz4KICAgIDxwYXRoIGNsYXNzPSJqcC1pY29uLWFjY2VudDIganAtaWNvbi1zZWxlY3RhYmxlLWludmVyc2UiIGQ9Ik01LjA1NjY0IDguNzYxNzJDNS4wNTY2NCA4LjU5NzY2IDUuMDMxMjUgOC40NTMxMiA0Ljk4MDQ3IDguMzI4MTJDNC45MzM1OSA4LjE5OTIyIDQuODU1NDcgOC4wODIwMyA0Ljc0NjA5IDcuOTc2NTZDNC42NDA2MiA3Ljg3MTA5IDQuNSA3Ljc3NTM5IDQuMzI0MjIgNy42ODk0NUM0LjE1MjM0IDcuNTk5NjEgMy45NDMzNiA3LjUxMTcyIDMuNjk3MjcgNy40MjU3OEMzLjMwMjczIDcuMjg1MTYgMi45NDMzNiA3LjEzNjcyIDIuNjE5MTQgNi45ODA0N0MyLjI5NDkyIDYuODI0MjIgMi4wMTc1OCA2LjY0MjU4IDEuNzg3MTEgNi40MzU1NUMxLjU2MDU1IDYuMjI4NTIgMS4zODQ3NyA1Ljk4ODI4IDEuMjU5NzcgNS43MTQ4NEMxLjEzNDc3IDUuNDM3NSAxLjA3MjI3IDUuMTA5MzggMS4wNzIyNyA0LjczMDQ3QzEuMDcyMjcgNC4zOTg0NCAxLjEyODkxIDQuMDk1NyAxLjI0MjE5IDMuODIyMjdDMS4zNTU0NyAzLjU0NDkyIDEuNTE1NjIgMy4zMDQ2OSAxLjcyMjY2IDMuMTAxNTZDMS45Mjk2OSAyLjg5ODQ0IDIuMTc5NjkgMi43MzQzNyAyLjQ3MjY2IDIuNjA5MzhDMi43NjU2MiAyLjQ4NDM4IDMuMDkxOCAyLjQwNDMgMy40NTExNyAyLjM2OTE0VjEuMTA5MzhINC4zODg2N1YyLjM4MDg2QzQuNzQwMjMgMi40Mjc3MyA1LjA1NjY0IDIuNTIzNDQgNS4zMzc4OSAyLjY2Nzk3QzUuNjE5MTQgMi44MTI1IDUuODU3NDIgMy4wMDE5NSA2LjA1MjczIDMuMjM2MzNDNi4yNTE5NSAzLjQ2NjggNi40MDQzIDMuNzQwMjMgNi41MDk3NyA0LjA1NjY0QzYuNjE5MTQgNC4zNjkxNCA2LjY3MzgzIDQuNzIwNyA2LjY3MzgzIDUuMTExMzNINS4wNDQ5MkM1LjA0NDkyIDQuNjM4NjcgNC45Mzc1IDQuMjgxMjUgNC43MjI2NiA0LjAzOTA2QzQuNTA3ODEgMy43OTI5NyA0LjIxNjggMy42Njk5MiAzLjg0OTYxIDMuNjY5OTJDMy42NTAzOSAzLjY2OTkyIDMuNDc2NTYgMy42OTcyNyAzLjMyODEyIDMuNzUxOTVDMy4xODM1OSAzLjgwMjczIDMuMDY0NDUgMy44NzY5NSAyLjk3MDcgMy45NzQ2MUMyLjg3Njk1IDQuMDY4MzYgMi44MDY2NCA0LjE3OTY5IDIuNzU5NzcgNC4zMDg1OUMyLjcxNjggNC40Mzc1IDIuNjk1MzEgNC41NzgxMiAyLjY5NTMxIDQuNzMwNDdDMi42OTUzMSA0Ljg4MjgxIDIuNzE2OCA1LjAxOTUzIDIuNzU5NzcgNS4xNDA2MkMyLjgwNjY0IDUuMjU3ODEgMi44ODI4MSA1LjM2NzE5IDIuOTg4MjggNS40Njg3NUMzLjA5NzY2IDUuNTcwMzEgMy4yNDAyMyA1LjY2Nzk3IDMuNDE2MDIgNS43NjE3MkMzLjU5MTggNS44NTE1NiAzLjgxMDU1IDUuOTQzMzYgNC4wNzIyNyA2LjAzNzExQzQuNDY2OCA2LjE4NTU1IDQuODI0MjIgNi4zMzk4NCA1LjE0NDUzIDYuNUM1LjQ2NDg0IDYuNjU2MjUgNS43MzgyOCA2LjgzOTg0IDUuOTY0ODQgNy4wNTA3OEM2LjE5NTMxIDcuMjU3ODEgNi4zNzEwOSA3LjUgNi40OTIxOSA3Ljc3NzM0QzYuNjE3MTkgOC4wNTA3OCA2LjY3OTY5IDguMzc1IDYuNjc5NjkgOC43NUM2LjY3OTY5IDkuMDkzNzUgNi42MjMwNSA5LjQwNDMgNi41MDk3NyA5LjY4MTY0QzYuMzk2NDggOS45NTUwOCA2LjIzNDM4IDEwLjE5MTQgNi4wMjM0NCAxMC4zOTA2QzUuODEyNSAxMC41ODk4IDUuNTU4NTkgMTAuNzUgNS4yNjE3MiAxMC44NzExQzQuOTY0ODQgMTAuOTg4MyA0LjYzMjgxIDExLjA2NDUgNC4yNjU2MiAxMS4wOTk2VjEyLjI0OEgzLjMzMzk4VjExLjA5OTZDMy4wMDE5NSAxMS4wNjg0IDIuNjc5NjkgMTAuOTk2MSAyLjM2NzE5IDEwLjg4MjhDMi4wNTQ2OSAxMC43NjU2IDEuNzc3MzQgMTAuNTk3NyAxLjUzNTE2IDEwLjM3ODlDMS4yOTY4OCAxMC4xNjAyIDEuMTA1NDcgOS44ODQ3NyAwLjk2MDkzOCA5LjU1MjczQzAuODE2NDA2IDkuMjE2OCAwLjc0NDE0MSA4LjgxNDQ1IDAuNzQ0MTQxIDguMzQ1N0gyLjM3ODkxQzIuMzc4OTEgOC42MjY5NSAyLjQxOTkyIDguODYzMjggMi41MDE5NSA5LjA1NDY5QzIuNTgzOTggOS4yNDIxOSAyLjY4OTQ1IDkuMzkyNTggMi44MTgzNiA5LjUwNTg2QzIuOTUxMTcgOS42MTUyMyAzLjEwMTU2IDkuNjkzMzYgMy4yNjk1MyA5Ljc0MDIzQzMuNDM3NSA5Ljc4NzExIDMuNjA5MzggOS44MTA1NSAzLjc4NTE2IDkuODEwNTVDNC4yMDMxMiA5LjgxMDU1IDQuNTE5NTMgOS43MTI4OSA0LjczNDM4IDkuNTE3NThDNC45NDkyMiA5LjMyMjI3IDUuMDU2NjQgOS4wNzAzMSA1LjA1NjY0IDguNzYxNzJaTTEzLjQxOCAxMi4yNzE1SDguMDc0MjJWMTFIMTMuNDE4VjEyLjI3MTVaIiB0cmFuc2Zvcm09InRyYW5zbGF0ZSgzLjk1MjY0IDYpIiBmaWxsPSJ3aGl0ZSIvPgo8L3N2Zz4K);
  --jp-icon-text-editor: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8cGF0aCBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIiBkPSJNMTUgMTVIM3YyaDEydi0yem0wLThIM3YyaDEyVjd6TTMgMTNoMTh2LTJIM3Yyem0wIDhoMTh2LTJIM3Yyek0zIDN2MmgxOFYzSDN6Ii8+Cjwvc3ZnPgo=);
  --jp-icon-toc: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIyNCIgaGVpZ2h0PSIyNCIgdmlld0JveD0iMCAwIDI0IDI0Ij4KICA8ZyBjbGFzcz0ianAtaWNvbjMganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjNjE2MTYxIj4KICAgIDxwYXRoIGQ9Ik03LDVIMjFWN0g3VjVNNywxM1YxMUgyMVYxM0g3TTQsNC41QTEuNSwxLjUgMCAwLDEgNS41LDZBMS41LDEuNSAwIDAsMSA0LDcuNUExLjUsMS41IDAgMCwxIDIuNSw2QTEuNSwxLjUgMCAwLDEgNCw0LjVNNCwxMC41QTEuNSwxLjUgMCAwLDEgNS41LDEyQTEuNSwxLjUgMCAwLDEgNCwxMy41QTEuNSwxLjUgMCAwLDEgMi41LDEyQTEuNSwxLjUgMCAwLDEgNCwxMC41TTcsMTlWMTdIMjFWMTlIN000LDE2LjVBMS41LDEuNSAwIDAsMSA1LjUsMThBMS41LDEuNSAwIDAsMSA0LDE5LjVBMS41LDEuNSAwIDAsMSAyLjUsMThBMS41LDEuNSAwIDAsMSA0LDE2LjVaIiAvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-tree-view: url(data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjI0IiB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIyNCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICAgIDxnIGNsYXNzPSJqcC1pY29uMyIgZmlsbD0iIzYxNjE2MSI+CiAgICAgICAgPHBhdGggZD0iTTAgMGgyNHYyNEgweiIgZmlsbD0ibm9uZSIvPgogICAgICAgIDxwYXRoIGQ9Ik0yMiAxMVYzaC03djNIOVYzSDJ2OGg3VjhoMnYxMGg0djNoN3YtOGgtN3YzaC0yVjhoMnYzeiIvPgogICAgPC9nPgo8L3N2Zz4=);
  --jp-icon-trusted: url(data:image/svg+xml;base64,PHN2ZyBmaWxsPSJub25lIiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDI0IDI1Ij4KICAgIDxwYXRoIGNsYXNzPSJqcC1pY29uMiIgc3Ryb2tlPSIjMzMzMzMzIiBzdHJva2Utd2lkdGg9IjIiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDIgMykiIGQ9Ik0xLjg2MDk0IDExLjQ0MDlDMC44MjY0NDggOC43NzAyNyAwLjg2Mzc3OSA2LjA1NzY0IDEuMjQ5MDcgNC4xOTkzMkMyLjQ4MjA2IDMuOTMzNDcgNC4wODA2OCAzLjQwMzQ3IDUuNjAxMDIgMi44NDQ5QzcuMjM1NDkgMi4yNDQ0IDguODU2NjYgMS41ODE1IDkuOTg3NiAxLjA5NTM5QzExLjA1OTcgMS41ODM0MSAxMi42MDk0IDIuMjQ0NCAxNC4yMTggMi44NDMzOUMxNS43NTAzIDMuNDEzOTQgMTcuMzk5NSAzLjk1MjU4IDE4Ljc1MzkgNC4yMTM4NUMxOS4xMzY0IDYuMDcxNzcgMTkuMTcwOSA4Ljc3NzIyIDE4LjEzOSAxMS40NDA5QzE3LjAzMDMgMTQuMzAzMiAxNC42NjY4IDE3LjE4NDQgOS45OTk5OSAxOC45MzU0QzUuMzMzMiAxNy4xODQ0IDIuOTY5NjggMTQuMzAzMiAxLjg2MDk0IDExLjQ0MDlaIi8+CiAgICA8cGF0aCBjbGFzcz0ianAtaWNvbjIiIGZpbGw9IiMzMzMzMzMiIHN0cm9rZT0iIzMzMzMzMyIgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoOCA5Ljg2NzE5KSIgZD0iTTIuODYwMTUgNC44NjUzNUwwLjcyNjU0OSAyLjk5OTU5TDAgMy42MzA0NUwyLjg2MDE1IDYuMTMxNTdMOCAwLjYzMDg3Mkw3LjI3ODU3IDBMMi44NjAxNSA0Ljg2NTM1WiIvPgo8L3N2Zz4K);
  --jp-icon-undo: url(data:image/svg+xml;base64,PHN2ZyB2aWV3Qm94PSIwIDAgMjQgMjQiIHdpZHRoPSIxNiIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KICA8ZyBjbGFzcz0ianAtaWNvbjMiIGZpbGw9IiM2MTYxNjEiPgogICAgPHBhdGggZD0iTTEyLjUgOGMtMi42NSAwLTUuMDUuOTktNi45IDIuNkwyIDd2OWg5bC0zLjYyLTMuNjJjMS4zOS0xLjE2IDMuMTYtMS44OCA1LjEyLTEuODggMy41NCAwIDYuNTUgMi4zMSA3LjYgNS41bDIuMzctLjc4QzIxLjA4IDExLjAzIDE3LjE1IDggMTIuNSA4eiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-vega: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8ZyBjbGFzcz0ianAtaWNvbjEganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjMjEyMTIxIj4KICAgIDxwYXRoIGQ9Ik0xMC42IDUuNGwyLjItMy4ySDIuMnY3LjNsNC02LjZ6Ii8+CiAgICA8cGF0aCBkPSJNMTUuOCAyLjJsLTQuNCA2LjZMNyA2LjNsLTQuOCA4djUuNWgxNy42VjIuMmgtNHptLTcgMTUuNEg1LjV2LTQuNGgzLjN2NC40em00LjQgMEg5LjhWOS44aDMuNHY3Ljh6bTQuNCAwaC0zLjRWNi41aDMuNHYxMS4xeiIvPgogIDwvZz4KPC9zdmc+Cg==);
  --jp-icon-yaml: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgdmlld0JveD0iMCAwIDIyIDIyIj4KICA8ZyBjbGFzcz0ianAtaWNvbi1jb250cmFzdDIganAtaWNvbi1zZWxlY3RhYmxlIiBmaWxsPSIjRDgxQjYwIj4KICAgIDxwYXRoIGQ9Ik03LjIgMTguNnYtNS40TDMgNS42aDMuM2wxLjQgMy4xYy4zLjkuNiAxLjYgMSAyLjUuMy0uOC42LTEuNiAxLTIuNWwxLjQtMy4xaDMuNGwtNC40IDcuNnY1LjVsLTIuOS0uMXoiLz4KICAgIDxjaXJjbGUgY2xhc3M9InN0MCIgY3g9IjE3LjYiIGN5PSIxNi41IiByPSIyLjEiLz4KICAgIDxjaXJjbGUgY2xhc3M9InN0MCIgY3g9IjE3LjYiIGN5PSIxMSIgcj0iMi4xIi8+CiAgPC9nPgo8L3N2Zz4K);
}

/* Icon CSS class declarations */

.jp-AddIcon {
  background-image: var(--jp-icon-add);
}
.jp-BugIcon {
  background-image: var(--jp-icon-bug);
}
.jp-BuildIcon {
  background-image: var(--jp-icon-build);
}
.jp-CaretDownEmptyIcon {
  background-image: var(--jp-icon-caret-down-empty);
}
.jp-CaretDownEmptyThinIcon {
  background-image: var(--jp-icon-caret-down-empty-thin);
}
.jp-CaretDownIcon {
  background-image: var(--jp-icon-caret-down);
}
.jp-CaretLeftIcon {
  background-image: var(--jp-icon-caret-left);
}
.jp-CaretRightIcon {
  background-image: var(--jp-icon-caret-right);
}
.jp-CaretUpEmptyThinIcon {
  background-image: var(--jp-icon-caret-up-empty-thin);
}
.jp-CaretUpIcon {
  background-image: var(--jp-icon-caret-up);
}
.jp-CaseSensitiveIcon {
  background-image: var(--jp-icon-case-sensitive);
}
.jp-CheckIcon {
  background-image: var(--jp-icon-check);
}
.jp-CircleEmptyIcon {
  background-image: var(--jp-icon-circle-empty);
}
.jp-CircleIcon {
  background-image: var(--jp-icon-circle);
}
.jp-ClearIcon {
  background-image: var(--jp-icon-clear);
}
.jp-CloseIcon {
  background-image: var(--jp-icon-close);
}
.jp-CodeIcon {
  background-image: var(--jp-icon-code);
}
.jp-ConsoleIcon {
  background-image: var(--jp-icon-console);
}
.jp-CopyIcon {
  background-image: var(--jp-icon-copy);
}
.jp-CopyrightIcon {
  background-image: var(--jp-icon-copyright);
}
.jp-CutIcon {
  background-image: var(--jp-icon-cut);
}
.jp-DownloadIcon {
  background-image: var(--jp-icon-download);
}
.jp-EditIcon {
  background-image: var(--jp-icon-edit);
}
.jp-EllipsesIcon {
  background-image: var(--jp-icon-ellipses);
}
.jp-ExtensionIcon {
  background-image: var(--jp-icon-extension);
}
.jp-FastForwardIcon {
  background-image: var(--jp-icon-fast-forward);
}
.jp-FileIcon {
  background-image: var(--jp-icon-file);
}
.jp-FileUploadIcon {
  background-image: var(--jp-icon-file-upload);
}
.jp-FilterListIcon {
  background-image: var(--jp-icon-filter-list);
}
.jp-FolderIcon {
  background-image: var(--jp-icon-folder);
}
.jp-Html5Icon {
  background-image: var(--jp-icon-html5);
}
.jp-ImageIcon {
  background-image: var(--jp-icon-image);
}
.jp-InspectorIcon {
  background-image: var(--jp-icon-inspector);
}
.jp-JsonIcon {
  background-image: var(--jp-icon-json);
}
.jp-JuliaIcon {
  background-image: var(--jp-icon-julia);
}
.jp-JupyterFaviconIcon {
  background-image: var(--jp-icon-jupyter-favicon);
}
.jp-JupyterIcon {
  background-image: var(--jp-icon-jupyter);
}
.jp-JupyterlabWordmarkIcon {
  background-image: var(--jp-icon-jupyterlab-wordmark);
}
.jp-KernelIcon {
  background-image: var(--jp-icon-kernel);
}
.jp-KeyboardIcon {
  background-image: var(--jp-icon-keyboard);
}
.jp-LauncherIcon {
  background-image: var(--jp-icon-launcher);
}
.jp-LineFormIcon {
  background-image: var(--jp-icon-line-form);
}
.jp-LinkIcon {
  background-image: var(--jp-icon-link);
}
.jp-ListIcon {
  background-image: var(--jp-icon-list);
}
.jp-ListingsInfoIcon {
  background-image: var(--jp-icon-listings-info);
}
.jp-MarkdownIcon {
  background-image: var(--jp-icon-markdown);
}
.jp-NewFolderIcon {
  background-image: var(--jp-icon-new-folder);
}
.jp-NotTrustedIcon {
  background-image: var(--jp-icon-not-trusted);
}
.jp-NotebookIcon {
  background-image: var(--jp-icon-notebook);
}
.jp-NumberingIcon {
  background-image: var(--jp-icon-numbering);
}
.jp-OfflineBoltIcon {
  background-image: var(--jp-icon-offline-bolt);
}
.jp-PaletteIcon {
  background-image: var(--jp-icon-palette);
}
.jp-PasteIcon {
  background-image: var(--jp-icon-paste);
}
.jp-PdfIcon {
  background-image: var(--jp-icon-pdf);
}
.jp-PythonIcon {
  background-image: var(--jp-icon-python);
}
.jp-RKernelIcon {
  background-image: var(--jp-icon-r-kernel);
}
.jp-ReactIcon {
  background-image: var(--jp-icon-react);
}
.jp-RedoIcon {
  background-image: var(--jp-icon-redo);
}
.jp-RefreshIcon {
  background-image: var(--jp-icon-refresh);
}
.jp-RegexIcon {
  background-image: var(--jp-icon-regex);
}
.jp-RunIcon {
  background-image: var(--jp-icon-run);
}
.jp-RunningIcon {
  background-image: var(--jp-icon-running);
}
.jp-SaveIcon {
  background-image: var(--jp-icon-save);
}
.jp-SearchIcon {
  background-image: var(--jp-icon-search);
}
.jp-SettingsIcon {
  background-image: var(--jp-icon-settings);
}
.jp-SpreadsheetIcon {
  background-image: var(--jp-icon-spreadsheet);
}
.jp-StopIcon {
  background-image: var(--jp-icon-stop);
}
.jp-TabIcon {
  background-image: var(--jp-icon-tab);
}
.jp-TableRowsIcon {
  background-image: var(--jp-icon-table-rows);
}
.jp-TagIcon {
  background-image: var(--jp-icon-tag);
}
.jp-TerminalIcon {
  background-image: var(--jp-icon-terminal);
}
.jp-TextEditorIcon {
  background-image: var(--jp-icon-text-editor);
}
.jp-TocIcon {
  background-image: var(--jp-icon-toc);
}
.jp-TreeViewIcon {
  background-image: var(--jp-icon-tree-view);
}
.jp-TrustedIcon {
  background-image: var(--jp-icon-trusted);
}
.jp-UndoIcon {
  background-image: var(--jp-icon-undo);
}
.jp-VegaIcon {
  background-image: var(--jp-icon-vega);
}
.jp-YamlIcon {
  background-image: var(--jp-icon-yaml);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/**
 * (DEPRECATED) Support for consuming icons as CSS background images
 */

.jp-Icon,
.jp-MaterialIcon {
  background-position: center;
  background-repeat: no-repeat;
  background-size: 16px;
  min-width: 16px;
  min-height: 16px;
}

.jp-Icon-cover {
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
}

/**
 * (DEPRECATED) Support for specific CSS icon sizes
 */

.jp-Icon-16 {
  background-size: 16px;
  min-width: 16px;
  min-height: 16px;
}

.jp-Icon-18 {
  background-size: 18px;
  min-width: 18px;
  min-height: 18px;
}

.jp-Icon-20 {
  background-size: 20px;
  min-width: 20px;
  min-height: 20px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/**
 * Support for icons as inline SVG HTMLElements
 */

/* recolor the primary elements of an icon */
.jp-icon0[fill] {
  fill: var(--jp-inverse-layout-color0);
}
.jp-icon1[fill] {
  fill: var(--jp-inverse-layout-color1);
}
.jp-icon2[fill] {
  fill: var(--jp-inverse-layout-color2);
}
.jp-icon3[fill] {
  fill: var(--jp-inverse-layout-color3);
}
.jp-icon4[fill] {
  fill: var(--jp-inverse-layout-color4);
}

.jp-icon0[stroke] {
  stroke: var(--jp-inverse-layout-color0);
}
.jp-icon1[stroke] {
  stroke: var(--jp-inverse-layout-color1);
}
.jp-icon2[stroke] {
  stroke: var(--jp-inverse-layout-color2);
}
.jp-icon3[stroke] {
  stroke: var(--jp-inverse-layout-color3);
}
.jp-icon4[stroke] {
  stroke: var(--jp-inverse-layout-color4);
}
/* recolor the accent elements of an icon */
.jp-icon-accent0[fill] {
  fill: var(--jp-layout-color0);
}
.jp-icon-accent1[fill] {
  fill: var(--jp-layout-color1);
}
.jp-icon-accent2[fill] {
  fill: var(--jp-layout-color2);
}
.jp-icon-accent3[fill] {
  fill: var(--jp-layout-color3);
}
.jp-icon-accent4[fill] {
  fill: var(--jp-layout-color4);
}

.jp-icon-accent0[stroke] {
  stroke: var(--jp-layout-color0);
}
.jp-icon-accent1[stroke] {
  stroke: var(--jp-layout-color1);
}
.jp-icon-accent2[stroke] {
  stroke: var(--jp-layout-color2);
}
.jp-icon-accent3[stroke] {
  stroke: var(--jp-layout-color3);
}
.jp-icon-accent4[stroke] {
  stroke: var(--jp-layout-color4);
}
/* set the color of an icon to transparent */
.jp-icon-none[fill] {
  fill: none;
}

.jp-icon-none[stroke] {
  stroke: none;
}
/* brand icon colors. Same for light and dark */
.jp-icon-brand0[fill] {
  fill: var(--jp-brand-color0);
}
.jp-icon-brand1[fill] {
  fill: var(--jp-brand-color1);
}
.jp-icon-brand2[fill] {
  fill: var(--jp-brand-color2);
}
.jp-icon-brand3[fill] {
  fill: var(--jp-brand-color3);
}
.jp-icon-brand4[fill] {
  fill: var(--jp-brand-color4);
}

.jp-icon-brand0[stroke] {
  stroke: var(--jp-brand-color0);
}
.jp-icon-brand1[stroke] {
  stroke: var(--jp-brand-color1);
}
.jp-icon-brand2[stroke] {
  stroke: var(--jp-brand-color2);
}
.jp-icon-brand3[stroke] {
  stroke: var(--jp-brand-color3);
}
.jp-icon-brand4[stroke] {
  stroke: var(--jp-brand-color4);
}
/* warn icon colors. Same for light and dark */
.jp-icon-warn0[fill] {
  fill: var(--jp-warn-color0);
}
.jp-icon-warn1[fill] {
  fill: var(--jp-warn-color1);
}
.jp-icon-warn2[fill] {
  fill: var(--jp-warn-color2);
}
.jp-icon-warn3[fill] {
  fill: var(--jp-warn-color3);
}

.jp-icon-warn0[stroke] {
  stroke: var(--jp-warn-color0);
}
.jp-icon-warn1[stroke] {
  stroke: var(--jp-warn-color1);
}
.jp-icon-warn2[stroke] {
  stroke: var(--jp-warn-color2);
}
.jp-icon-warn3[stroke] {
  stroke: var(--jp-warn-color3);
}
/* icon colors that contrast well with each other and most backgrounds */
.jp-icon-contrast0[fill] {
  fill: var(--jp-icon-contrast-color0);
}
.jp-icon-contrast1[fill] {
  fill: var(--jp-icon-contrast-color1);
}
.jp-icon-contrast2[fill] {
  fill: var(--jp-icon-contrast-color2);
}
.jp-icon-contrast3[fill] {
  fill: var(--jp-icon-contrast-color3);
}

.jp-icon-contrast0[stroke] {
  stroke: var(--jp-icon-contrast-color0);
}
.jp-icon-contrast1[stroke] {
  stroke: var(--jp-icon-contrast-color1);
}
.jp-icon-contrast2[stroke] {
  stroke: var(--jp-icon-contrast-color2);
}
.jp-icon-contrast3[stroke] {
  stroke: var(--jp-icon-contrast-color3);
}

/* CSS for icons in selected items in the settings editor */
#setting-editor .jp-PluginList .jp-mod-selected .jp-icon-selectable[fill] {
  fill: #fff;
}
#setting-editor
  .jp-PluginList
  .jp-mod-selected
  .jp-icon-selectable-inverse[fill] {
  fill: var(--jp-brand-color1);
}

/* CSS for icons in selected filebrowser listing items */
.jp-DirListing-item.jp-mod-selected .jp-icon-selectable[fill] {
  fill: #fff;
}
.jp-DirListing-item.jp-mod-selected .jp-icon-selectable-inverse[fill] {
  fill: var(--jp-brand-color1);
}

/* CSS for icons in selected tabs in the sidebar tab manager */
#tab-manager .lm-TabBar-tab.jp-mod-active .jp-icon-selectable[fill] {
  fill: #fff;
}

#tab-manager .lm-TabBar-tab.jp-mod-active .jp-icon-selectable-inverse[fill] {
  fill: var(--jp-brand-color1);
}
#tab-manager
  .lm-TabBar-tab.jp-mod-active
  .jp-icon-hover
  :hover
  .jp-icon-selectable[fill] {
  fill: var(--jp-brand-color1);
}

#tab-manager
  .lm-TabBar-tab.jp-mod-active
  .jp-icon-hover
  :hover
  .jp-icon-selectable-inverse[fill] {
  fill: #fff;
}

/**
 * TODO: come up with non css-hack solution for showing the busy icon on top
 *  of the close icon
 * CSS for complex behavior of close icon of tabs in the sidebar tab manager
 */
#tab-manager
  .lm-TabBar-tab.jp-mod-dirty
  > .lm-TabBar-tabCloseIcon
  > :not(:hover)
  > .jp-icon3[fill] {
  fill: none;
}
#tab-manager
  .lm-TabBar-tab.jp-mod-dirty
  > .lm-TabBar-tabCloseIcon
  > :not(:hover)
  > .jp-icon-busy[fill] {
  fill: var(--jp-inverse-layout-color3);
}

#tab-manager
  .lm-TabBar-tab.jp-mod-dirty.jp-mod-active
  > .lm-TabBar-tabCloseIcon
  > :not(:hover)
  > .jp-icon-busy[fill] {
  fill: #fff;
}

/**
* TODO: come up with non css-hack solution for showing the busy icon on top
*  of the close icon
* CSS for complex behavior of close icon of tabs in the main area tabbar
*/
.lm-DockPanel-tabBar
  .lm-TabBar-tab.lm-mod-closable.jp-mod-dirty
  > .lm-TabBar-tabCloseIcon
  > :not(:hover)
  > .jp-icon3[fill] {
  fill: none;
}
.lm-DockPanel-tabBar
  .lm-TabBar-tab.lm-mod-closable.jp-mod-dirty
  > .lm-TabBar-tabCloseIcon
  > :not(:hover)
  > .jp-icon-busy[fill] {
  fill: var(--jp-inverse-layout-color3);
}

/* CSS for icons in status bar */
#jp-main-statusbar .jp-mod-selected .jp-icon-selectable[fill] {
  fill: #fff;
}

#jp-main-statusbar .jp-mod-selected .jp-icon-selectable-inverse[fill] {
  fill: var(--jp-brand-color1);
}
/* special handling for splash icon CSS. While the theme CSS reloads during
   splash, the splash icon can loose theming. To prevent that, we set a
   default for its color variable */
:root {
  --jp-warn-color0: var(--md-orange-700);
}

/* not sure what to do with this one, used in filebrowser listing */
.jp-DragIcon {
  margin-right: 4px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/**
 * Support for alt colors for icons as inline SVG HTMLElements
 */

/* alt recolor the primary elements of an icon */
.jp-icon-alt .jp-icon0[fill] {
  fill: var(--jp-layout-color0);
}
.jp-icon-alt .jp-icon1[fill] {
  fill: var(--jp-layout-color1);
}
.jp-icon-alt .jp-icon2[fill] {
  fill: var(--jp-layout-color2);
}
.jp-icon-alt .jp-icon3[fill] {
  fill: var(--jp-layout-color3);
}
.jp-icon-alt .jp-icon4[fill] {
  fill: var(--jp-layout-color4);
}

.jp-icon-alt .jp-icon0[stroke] {
  stroke: var(--jp-layout-color0);
}
.jp-icon-alt .jp-icon1[stroke] {
  stroke: var(--jp-layout-color1);
}
.jp-icon-alt .jp-icon2[stroke] {
  stroke: var(--jp-layout-color2);
}
.jp-icon-alt .jp-icon3[stroke] {
  stroke: var(--jp-layout-color3);
}
.jp-icon-alt .jp-icon4[stroke] {
  stroke: var(--jp-layout-color4);
}

/* alt recolor the accent elements of an icon */
.jp-icon-alt .jp-icon-accent0[fill] {
  fill: var(--jp-inverse-layout-color0);
}
.jp-icon-alt .jp-icon-accent1[fill] {
  fill: var(--jp-inverse-layout-color1);
}
.jp-icon-alt .jp-icon-accent2[fill] {
  fill: var(--jp-inverse-layout-color2);
}
.jp-icon-alt .jp-icon-accent3[fill] {
  fill: var(--jp-inverse-layout-color3);
}
.jp-icon-alt .jp-icon-accent4[fill] {
  fill: var(--jp-inverse-layout-color4);
}

.jp-icon-alt .jp-icon-accent0[stroke] {
  stroke: var(--jp-inverse-layout-color0);
}
.jp-icon-alt .jp-icon-accent1[stroke] {
  stroke: var(--jp-inverse-layout-color1);
}
.jp-icon-alt .jp-icon-accent2[stroke] {
  stroke: var(--jp-inverse-layout-color2);
}
.jp-icon-alt .jp-icon-accent3[stroke] {
  stroke: var(--jp-inverse-layout-color3);
}
.jp-icon-alt .jp-icon-accent4[stroke] {
  stroke: var(--jp-inverse-layout-color4);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-icon-hoverShow:not(:hover) svg {
  display: none !important;
}

/**
 * Support for hover colors for icons as inline SVG HTMLElements
 */

/**
 * regular colors
 */

/* recolor the primary elements of an icon */
.jp-icon-hover :hover .jp-icon0-hover[fill] {
  fill: var(--jp-inverse-layout-color0);
}
.jp-icon-hover :hover .jp-icon1-hover[fill] {
  fill: var(--jp-inverse-layout-color1);
}
.jp-icon-hover :hover .jp-icon2-hover[fill] {
  fill: var(--jp-inverse-layout-color2);
}
.jp-icon-hover :hover .jp-icon3-hover[fill] {
  fill: var(--jp-inverse-layout-color3);
}
.jp-icon-hover :hover .jp-icon4-hover[fill] {
  fill: var(--jp-inverse-layout-color4);
}

.jp-icon-hover :hover .jp-icon0-hover[stroke] {
  stroke: var(--jp-inverse-layout-color0);
}
.jp-icon-hover :hover .jp-icon1-hover[stroke] {
  stroke: var(--jp-inverse-layout-color1);
}
.jp-icon-hover :hover .jp-icon2-hover[stroke] {
  stroke: var(--jp-inverse-layout-color2);
}
.jp-icon-hover :hover .jp-icon3-hover[stroke] {
  stroke: var(--jp-inverse-layout-color3);
}
.jp-icon-hover :hover .jp-icon4-hover[stroke] {
  stroke: var(--jp-inverse-layout-color4);
}

/* recolor the accent elements of an icon */
.jp-icon-hover :hover .jp-icon-accent0-hover[fill] {
  fill: var(--jp-layout-color0);
}
.jp-icon-hover :hover .jp-icon-accent1-hover[fill] {
  fill: var(--jp-layout-color1);
}
.jp-icon-hover :hover .jp-icon-accent2-hover[fill] {
  fill: var(--jp-layout-color2);
}
.jp-icon-hover :hover .jp-icon-accent3-hover[fill] {
  fill: var(--jp-layout-color3);
}
.jp-icon-hover :hover .jp-icon-accent4-hover[fill] {
  fill: var(--jp-layout-color4);
}

.jp-icon-hover :hover .jp-icon-accent0-hover[stroke] {
  stroke: var(--jp-layout-color0);
}
.jp-icon-hover :hover .jp-icon-accent1-hover[stroke] {
  stroke: var(--jp-layout-color1);
}
.jp-icon-hover :hover .jp-icon-accent2-hover[stroke] {
  stroke: var(--jp-layout-color2);
}
.jp-icon-hover :hover .jp-icon-accent3-hover[stroke] {
  stroke: var(--jp-layout-color3);
}
.jp-icon-hover :hover .jp-icon-accent4-hover[stroke] {
  stroke: var(--jp-layout-color4);
}

/* set the color of an icon to transparent */
.jp-icon-hover :hover .jp-icon-none-hover[fill] {
  fill: none;
}

.jp-icon-hover :hover .jp-icon-none-hover[stroke] {
  stroke: none;
}

/**
 * inverse colors
 */

/* inverse recolor the primary elements of an icon */
.jp-icon-hover.jp-icon-alt :hover .jp-icon0-hover[fill] {
  fill: var(--jp-layout-color0);
}
.jp-icon-hover.jp-icon-alt :hover .jp-icon1-hover[fill] {
  fill: var(--jp-layout-color1);
}
.jp-icon-hover.jp-icon-alt :hover .jp-icon2-hover[fill] {
  fill: var(--jp-layout-color2);
}
.jp-icon-hover.jp-icon-alt :hover .jp-icon3-hover[fill] {
  fill: var(--jp-layout-color3);
}
.jp-icon-hover.jp-icon-alt :hover .jp-icon4-hover[fill] {
  fill: var(--jp-layout-color4);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon0-hover[stroke] {
  stroke: var(--jp-layout-color0);
}
.jp-icon-hover.jp-icon-alt :hover .jp-icon1-hover[stroke] {
  stroke: var(--jp-layout-color1);
}
.jp-icon-hover.jp-icon-alt :hover .jp-icon2-hover[stroke] {
  stroke: var(--jp-layout-color2);
}
.jp-icon-hover.jp-icon-alt :hover .jp-icon3-hover[stroke] {
  stroke: var(--jp-layout-color3);
}
.jp-icon-hover.jp-icon-alt :hover .jp-icon4-hover[stroke] {
  stroke: var(--jp-layout-color4);
}

/* inverse recolor the accent elements of an icon */
.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent0-hover[fill] {
  fill: var(--jp-inverse-layout-color0);
}
.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent1-hover[fill] {
  fill: var(--jp-inverse-layout-color1);
}
.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent2-hover[fill] {
  fill: var(--jp-inverse-layout-color2);
}
.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent3-hover[fill] {
  fill: var(--jp-inverse-layout-color3);
}
.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent4-hover[fill] {
  fill: var(--jp-inverse-layout-color4);
}

.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent0-hover[stroke] {
  stroke: var(--jp-inverse-layout-color0);
}
.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent1-hover[stroke] {
  stroke: var(--jp-inverse-layout-color1);
}
.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent2-hover[stroke] {
  stroke: var(--jp-inverse-layout-color2);
}
.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent3-hover[stroke] {
  stroke: var(--jp-inverse-layout-color3);
}
.jp-icon-hover.jp-icon-alt :hover .jp-icon-accent4-hover[stroke] {
  stroke: var(--jp-inverse-layout-color4);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-switch {
  display: flex;
  align-items: center;
  padding-left: 4px;
  padding-right: 4px;
  font-size: var(--jp-ui-font-size1);
  background-color: transparent;
  color: var(--jp-ui-font-color1);
  border: none;
  height: 20px;
}

.jp-switch:hover {
  background-color: var(--jp-layout-color2);
}

.jp-switch-label {
  margin-right: 5px;
}

.jp-switch-track {
  cursor: pointer;
  background-color: var(--jp-border-color1);
  -webkit-transition: 0.4s;
  transition: 0.4s;
  border-radius: 34px;
  height: 16px;
  width: 35px;
  position: relative;
}

.jp-switch-track::before {
  content: '';
  position: absolute;
  height: 10px;
  width: 10px;
  margin: 3px;
  left: 0px;
  background-color: var(--jp-ui-inverse-font-color1);
  -webkit-transition: 0.4s;
  transition: 0.4s;
  border-radius: 50%;
}

.jp-switch[aria-checked='true'] .jp-switch-track {
  background-color: var(--jp-warn-color0);
}

.jp-switch[aria-checked='true'] .jp-switch-track::before {
  /* track width (35) - margins (3 + 3) - thumb width (10) */
  left: 19px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/* Sibling imports */

/* Override Blueprint's _reset.scss styles */
html {
  box-sizing: unset;
}

*,
*::before,
*::after {
  box-sizing: unset;
}

body {
  color: unset;
  font-family: var(--jp-ui-font-family);
}

p {
  margin-top: unset;
  margin-bottom: unset;
}

small {
  font-size: unset;
}

strong {
  font-weight: unset;
}

/* Override Blueprint's _typography.scss styles */
a {
  text-decoration: unset;
  color: unset;
}
a:hover {
  text-decoration: unset;
  color: unset;
}

/* Override Blueprint's _accessibility.scss styles */
:focus {
  outline: unset;
  outline-offset: unset;
  -moz-outline-radius: unset;
}

/* Styles for ui-components */
.jp-Button {
  border-radius: var(--jp-border-radius);
  padding: 0px 12px;
  font-size: var(--jp-ui-font-size1);
}

/* Use our own theme for hover styles */
button.jp-Button.bp3-button.bp3-minimal:hover {
  background-color: var(--jp-layout-color2);
}
.jp-Button.minimal {
  color: unset !important;
}

.jp-Button.jp-ToolbarButtonComponent {
  text-transform: none;
}

.jp-InputGroup input {
  box-sizing: border-box;
  border-radius: 0;
  background-color: transparent;
  color: var(--jp-ui-font-color0);
  box-shadow: inset 0 0 0 var(--jp-border-width) var(--jp-input-border-color);
}

.jp-InputGroup input:focus {
  box-shadow: inset 0 0 0 var(--jp-border-width)
      var(--jp-input-active-box-shadow-color),
    inset 0 0 0 3px var(--jp-input-active-box-shadow-color);
}

.jp-InputGroup input::placeholder,
input::placeholder {
  color: var(--jp-ui-font-color3);
}

.jp-BPIcon {
  display: inline-block;
  vertical-align: middle;
  margin: auto;
}

/* Stop blueprint futzing with our icon fills */
.bp3-icon.jp-BPIcon > svg:not([fill]) {
  fill: var(--jp-inverse-layout-color3);
}

.jp-InputGroupAction {
  padding: 6px;
}

.jp-HTMLSelect.jp-DefaultStyle select {
  background-color: initial;
  border: none;
  border-radius: 0;
  box-shadow: none;
  color: var(--jp-ui-font-color0);
  display: block;
  font-size: var(--jp-ui-font-size1);
  height: 24px;
  line-height: 14px;
  padding: 0 25px 0 10px;
  text-align: left;
  -moz-appearance: none;
  -webkit-appearance: none;
}

/* Use our own theme for hover and option styles */
.jp-HTMLSelect.jp-DefaultStyle select:hover,
.jp-HTMLSelect.jp-DefaultStyle select > option {
  background-color: var(--jp-layout-color2);
  color: var(--jp-ui-font-color0);
}
select {
  box-sizing: border-box;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-Collapse {
  display: flex;
  flex-direction: column;
  align-items: stretch;
  border-top: 1px solid var(--jp-border-color2);
  border-bottom: 1px solid var(--jp-border-color2);
}

.jp-Collapse-header {
  padding: 1px 12px;
  color: var(--jp-ui-font-color1);
  background-color: var(--jp-layout-color1);
  font-size: var(--jp-ui-font-size2);
}

.jp-Collapse-header:hover {
  background-color: var(--jp-layout-color2);
}

.jp-Collapse-contents {
  padding: 0px 12px 0px 12px;
  background-color: var(--jp-layout-color1);
  color: var(--jp-ui-font-color1);
  overflow: auto;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Variables
|----------------------------------------------------------------------------*/

:root {
  --jp-private-commandpalette-search-height: 28px;
}

/*-----------------------------------------------------------------------------
| Overall styles
|----------------------------------------------------------------------------*/

.lm-CommandPalette {
  padding-bottom: 0px;
  color: var(--jp-ui-font-color1);
  background: var(--jp-layout-color1);
  /* This is needed so that all font sizing of children done in ems is
   * relative to this base size */
  font-size: var(--jp-ui-font-size1);
}

/*-----------------------------------------------------------------------------
| Modal variant
|----------------------------------------------------------------------------*/

.jp-ModalCommandPalette {
  position: absolute;
  z-index: 10000;
  top: 38px;
  left: 30%;
  margin: 0;
  padding: 4px;
  width: 40%;
  box-shadow: var(--jp-elevation-z4);
  border-radius: 4px;
  background: var(--jp-layout-color0);
}

.jp-ModalCommandPalette .lm-CommandPalette {
  max-height: 40vh;
}

.jp-ModalCommandPalette .lm-CommandPalette .lm-close-icon::after {
  display: none;
}

.jp-ModalCommandPalette .lm-CommandPalette .lm-CommandPalette-header {
  display: none;
}

.jp-ModalCommandPalette .lm-CommandPalette .lm-CommandPalette-item {
  margin-left: 4px;
  margin-right: 4px;
}

.jp-ModalCommandPalette
  .lm-CommandPalette
  .lm-CommandPalette-item.lm-mod-disabled {
  display: none;
}

/*-----------------------------------------------------------------------------
| Search
|----------------------------------------------------------------------------*/

.lm-CommandPalette-search {
  padding: 4px;
  background-color: var(--jp-layout-color1);
  z-index: 2;
}

.lm-CommandPalette-wrapper {
  overflow: overlay;
  padding: 0px 9px;
  background-color: var(--jp-input-active-background);
  height: 30px;
  box-shadow: inset 0 0 0 var(--jp-border-width) var(--jp-input-border-color);
}

.lm-CommandPalette.lm-mod-focused .lm-CommandPalette-wrapper {
  box-shadow: inset 0 0 0 1px var(--jp-input-active-box-shadow-color),
    inset 0 0 0 3px var(--jp-input-active-box-shadow-color);
}

.jp-SearchIconGroup {
  color: white;
  background-color: var(--jp-brand-color1);
  position: absolute;
  top: 4px;
  right: 4px;
  padding: 5px 5px 1px 5px;
}

.jp-SearchIconGroup svg {
  height: 20px;
  width: 20px;
}

.jp-SearchIconGroup .jp-icon3[fill] {
  fill: var(--jp-layout-color0);
}

.lm-CommandPalette-input {
  background: transparent;
  width: calc(100% - 18px);
  float: left;
  border: none;
  outline: none;
  font-size: var(--jp-ui-font-size1);
  color: var(--jp-ui-font-color0);
  line-height: var(--jp-private-commandpalette-search-height);
}

.lm-CommandPalette-input::-webkit-input-placeholder,
.lm-CommandPalette-input::-moz-placeholder,
.lm-CommandPalette-input:-ms-input-placeholder {
  color: var(--jp-ui-font-color2);
  font-size: var(--jp-ui-font-size1);
}

/*-----------------------------------------------------------------------------
| Results
|----------------------------------------------------------------------------*/

.lm-CommandPalette-header:first-child {
  margin-top: 0px;
}

.lm-CommandPalette-header {
  border-bottom: solid var(--jp-border-width) var(--jp-border-color2);
  color: var(--jp-ui-font-color1);
  cursor: pointer;
  display: flex;
  font-size: var(--jp-ui-font-size0);
  font-weight: 600;
  letter-spacing: 1px;
  margin-top: 8px;
  padding: 8px 0 8px 12px;
  text-transform: uppercase;
}

.lm-CommandPalette-header.lm-mod-active {
  background: var(--jp-layout-color2);
}

.lm-CommandPalette-header > mark {
  background-color: transparent;
  font-weight: bold;
  color: var(--jp-ui-font-color1);
}

.lm-CommandPalette-item {
  padding: 4px 12px 4px 4px;
  color: var(--jp-ui-font-color1);
  font-size: var(--jp-ui-font-size1);
  font-weight: 400;
  display: flex;
}

.lm-CommandPalette-item.lm-mod-disabled {
  color: var(--jp-ui-font-color2);
}

.lm-CommandPalette-item.lm-mod-active {
  color: var(--jp-ui-inverse-font-color1);
  background: var(--jp-brand-color1);
}

.lm-CommandPalette-item.lm-mod-active .lm-CommandPalette-itemLabel > mark {
  color: var(--jp-ui-inverse-font-color0);
}

.lm-CommandPalette-item.lm-mod-active .jp-icon-selectable[fill] {
  fill: var(--jp-layout-color0);
}

.lm-CommandPalette-item.lm-mod-active .lm-CommandPalette-itemLabel > mark {
  color: var(--jp-ui-inverse-font-color0);
}

.lm-CommandPalette-item.lm-mod-active:hover:not(.lm-mod-disabled) {
  color: var(--jp-ui-inverse-font-color1);
  background: var(--jp-brand-color1);
}

.lm-CommandPalette-item:hover:not(.lm-mod-active):not(.lm-mod-disabled) {
  background: var(--jp-layout-color2);
}

.lm-CommandPalette-itemContent {
  overflow: hidden;
}

.lm-CommandPalette-itemLabel > mark {
  color: var(--jp-ui-font-color0);
  background-color: transparent;
  font-weight: bold;
}

.lm-CommandPalette-item.lm-mod-disabled mark {
  color: var(--jp-ui-font-color2);
}

.lm-CommandPalette-item .lm-CommandPalette-itemIcon {
  margin: 0 4px 0 0;
  position: relative;
  width: 16px;
  top: 2px;
  flex: 0 0 auto;
}

.lm-CommandPalette-item.lm-mod-disabled .lm-CommandPalette-itemIcon {
  opacity: 0.6;
}

.lm-CommandPalette-item .lm-CommandPalette-itemShortcut {
  flex: 0 0 auto;
}

.lm-CommandPalette-itemCaption {
  display: none;
}

.lm-CommandPalette-content {
  background-color: var(--jp-layout-color1);
}

.lm-CommandPalette-content:empty:after {
  content: 'No results';
  margin: auto;
  margin-top: 20px;
  width: 100px;
  display: block;
  font-size: var(--jp-ui-font-size2);
  font-family: var(--jp-ui-font-family);
  font-weight: lighter;
}

.lm-CommandPalette-emptyMessage {
  text-align: center;
  margin-top: 24px;
  line-height: 1.32;
  padding: 0px 8px;
  color: var(--jp-content-font-color3);
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-Dialog {
  position: absolute;
  z-index: 10000;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  top: 0px;
  left: 0px;
  margin: 0;
  padding: 0;
  width: 100%;
  height: 100%;
  background: var(--jp-dialog-background);
}

.jp-Dialog-content {
  display: flex;
  flex-direction: column;
  margin-left: auto;
  margin-right: auto;
  background: var(--jp-layout-color1);
  padding: 24px;
  padding-bottom: 12px;
  min-width: 300px;
  min-height: 150px;
  max-width: 1000px;
  max-height: 500px;
  box-sizing: border-box;
  box-shadow: var(--jp-elevation-z20);
  word-wrap: break-word;
  border-radius: var(--jp-border-radius);
  /* This is needed so that all font sizing of children done in ems is
   * relative to this base size */
  font-size: var(--jp-ui-font-size1);
  color: var(--jp-ui-font-color1);
  resize: both;
}

.jp-Dialog-button {
  overflow: visible;
}

button.jp-Dialog-button:focus {
  outline: 1px solid var(--jp-brand-color1);
  outline-offset: 4px;
  -moz-outline-radius: 0px;
}

button.jp-Dialog-button:focus::-moz-focus-inner {
  border: 0;
}

button.jp-Dialog-close-button {
  padding: 0;
  height: 100%;
  min-width: unset;
  min-height: unset;
}

.jp-Dialog-header {
  display: flex;
  justify-content: space-between;
  flex: 0 0 auto;
  padding-bottom: 12px;
  font-size: var(--jp-ui-font-size3);
  font-weight: 400;
  color: var(--jp-ui-font-color0);
}

.jp-Dialog-body {
  display: flex;
  flex-direction: column;
  flex: 1 1 auto;
  font-size: var(--jp-ui-font-size1);
  background: var(--jp-layout-color1);
  overflow: auto;
}

.jp-Dialog-footer {
  display: flex;
  flex-direction: row;
  justify-content: flex-end;
  flex: 0 0 auto;
  margin-left: -12px;
  margin-right: -12px;
  padding: 12px;
}

.jp-Dialog-title {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}

.jp-Dialog-body > .jp-select-wrapper {
  width: 100%;
}

.jp-Dialog-body > button {
  padding: 0px 16px;
}

.jp-Dialog-body > label {
  line-height: 1.4;
  color: var(--jp-ui-font-color0);
}

.jp-Dialog-button.jp-mod-styled:not(:last-child) {
  margin-right: 12px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2016, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-HoverBox {
  position: fixed;
}

.jp-HoverBox.jp-mod-outofview {
  display: none;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-IFrame {
  width: 100%;
  height: 100%;
}

.jp-IFrame > iframe {
  border: none;
}

/*
When drag events occur, `p-mod-override-cursor` is added to the body.
Because iframes steal all cursor events, the following two rules are necessary
to suppress pointer events while resize drags are occurring. There may be a
better solution to this problem.
*/
body.lm-mod-override-cursor .jp-IFrame {
  position: relative;
}

body.lm-mod-override-cursor .jp-IFrame:before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: transparent;
}

.jp-Input-Boolean-Dialog {
  flex-direction: row-reverse;
  align-items: end;
  width: 100%;
}

.jp-Input-Boolean-Dialog > label {
  flex: 1 1 auto;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2016, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-MainAreaWidget > :focus {
  outline: none;
}

/**
 * google-material-color v1.2.6
 * https://github.com/danlevan/google-material-color
 */
:root {
  --md-red-50: #ffebee;
  --md-red-100: #ffcdd2;
  --md-red-200: #ef9a9a;
  --md-red-300: #e57373;
  --md-red-400: #ef5350;
  --md-red-500: #f44336;
  --md-red-600: #e53935;
  --md-red-700: #d32f2f;
  --md-red-800: #c62828;
  --md-red-900: #b71c1c;
  --md-red-A100: #ff8a80;
  --md-red-A200: #ff5252;
  --md-red-A400: #ff1744;
  --md-red-A700: #d50000;

  --md-pink-50: #fce4ec;
  --md-pink-100: #f8bbd0;
  --md-pink-200: #f48fb1;
  --md-pink-300: #f06292;
  --md-pink-400: #ec407a;
  --md-pink-500: #e91e63;
  --md-pink-600: #d81b60;
  --md-pink-700: #c2185b;
  --md-pink-800: #ad1457;
  --md-pink-900: #880e4f;
  --md-pink-A100: #ff80ab;
  --md-pink-A200: #ff4081;
  --md-pink-A400: #f50057;
  --md-pink-A700: #c51162;

  --md-purple-50: #f3e5f5;
  --md-purple-100: #e1bee7;
  --md-purple-200: #ce93d8;
  --md-purple-300: #ba68c8;
  --md-purple-400: #ab47bc;
  --md-purple-500: #9c27b0;
  --md-purple-600: #8e24aa;
  --md-purple-700: #7b1fa2;
  --md-purple-800: #6a1b9a;
  --md-purple-900: #4a148c;
  --md-purple-A100: #ea80fc;
  --md-purple-A200: #e040fb;
  --md-purple-A400: #d500f9;
  --md-purple-A700: #aa00ff;

  --md-deep-purple-50: #ede7f6;
  --md-deep-purple-100: #d1c4e9;
  --md-deep-purple-200: #b39ddb;
  --md-deep-purple-300: #9575cd;
  --md-deep-purple-400: #7e57c2;
  --md-deep-purple-500: #673ab7;
  --md-deep-purple-600: #5e35b1;
  --md-deep-purple-700: #512da8;
  --md-deep-purple-800: #4527a0;
  --md-deep-purple-900: #311b92;
  --md-deep-purple-A100: #b388ff;
  --md-deep-purple-A200: #7c4dff;
  --md-deep-purple-A400: #651fff;
  --md-deep-purple-A700: #6200ea;

  --md-indigo-50: #e8eaf6;
  --md-indigo-100: #c5cae9;
  --md-indigo-200: #9fa8da;
  --md-indigo-300: #7986cb;
  --md-indigo-400: #5c6bc0;
  --md-indigo-500: #3f51b5;
  --md-indigo-600: #3949ab;
  --md-indigo-700: #303f9f;
  --md-indigo-800: #283593;
  --md-indigo-900: #1a237e;
  --md-indigo-A100: #8c9eff;
  --md-indigo-A200: #536dfe;
  --md-indigo-A400: #3d5afe;
  --md-indigo-A700: #304ffe;

  --md-blue-50: #e3f2fd;
  --md-blue-100: #bbdefb;
  --md-blue-200: #90caf9;
  --md-blue-300: #64b5f6;
  --md-blue-400: #42a5f5;
  --md-blue-500: #2196f3;
  --md-blue-600: #1e88e5;
  --md-blue-700: #1976d2;
  --md-blue-800: #1565c0;
  --md-blue-900: #0d47a1;
  --md-blue-A100: #82b1ff;
  --md-blue-A200: #448aff;
  --md-blue-A400: #2979ff;
  --md-blue-A700: #2962ff;

  --md-light-blue-50: #e1f5fe;
  --md-light-blue-100: #b3e5fc;
  --md-light-blue-200: #81d4fa;
  --md-light-blue-300: #4fc3f7;
  --md-light-blue-400: #29b6f6;
  --md-light-blue-500: #03a9f4;
  --md-light-blue-600: #039be5;
  --md-light-blue-700: #0288d1;
  --md-light-blue-800: #0277bd;
  --md-light-blue-900: #01579b;
  --md-light-blue-A100: #80d8ff;
  --md-light-blue-A200: #40c4ff;
  --md-light-blue-A400: #00b0ff;
  --md-light-blue-A700: #0091ea;

  --md-cyan-50: #e0f7fa;
  --md-cyan-100: #b2ebf2;
  --md-cyan-200: #80deea;
  --md-cyan-300: #4dd0e1;
  --md-cyan-400: #26c6da;
  --md-cyan-500: #00bcd4;
  --md-cyan-600: #00acc1;
  --md-cyan-700: #0097a7;
  --md-cyan-800: #00838f;
  --md-cyan-900: #006064;
  --md-cyan-A100: #84ffff;
  --md-cyan-A200: #18ffff;
  --md-cyan-A400: #00e5ff;
  --md-cyan-A700: #00b8d4;

  --md-teal-50: #e0f2f1;
  --md-teal-100: #b2dfdb;
  --md-teal-200: #80cbc4;
  --md-teal-300: #4db6ac;
  --md-teal-400: #26a69a;
  --md-teal-500: #009688;
  --md-teal-600: #00897b;
  --md-teal-700: #00796b;
  --md-teal-800: #00695c;
  --md-teal-900: #004d40;
  --md-teal-A100: #a7ffeb;
  --md-teal-A200: #64ffda;
  --md-teal-A400: #1de9b6;
  --md-teal-A700: #00bfa5;

  --md-green-50: #e8f5e9;
  --md-green-100: #c8e6c9;
  --md-green-200: #a5d6a7;
  --md-green-300: #81c784;
  --md-green-400: #66bb6a;
  --md-green-500: #4caf50;
  --md-green-600: #43a047;
  --md-green-700: #388e3c;
  --md-green-800: #2e7d32;
  --md-green-900: #1b5e20;
  --md-green-A100: #b9f6ca;
  --md-green-A200: #69f0ae;
  --md-green-A400: #00e676;
  --md-green-A700: #00c853;

  --md-light-green-50: #f1f8e9;
  --md-light-green-100: #dcedc8;
  --md-light-green-200: #c5e1a5;
  --md-light-green-300: #aed581;
  --md-light-green-400: #9ccc65;
  --md-light-green-500: #8bc34a;
  --md-light-green-600: #7cb342;
  --md-light-green-700: #689f38;
  --md-light-green-800: #558b2f;
  --md-light-green-900: #33691e;
  --md-light-green-A100: #ccff90;
  --md-light-green-A200: #b2ff59;
  --md-light-green-A400: #76ff03;
  --md-light-green-A700: #64dd17;

  --md-lime-50: #f9fbe7;
  --md-lime-100: #f0f4c3;
  --md-lime-200: #e6ee9c;
  --md-lime-300: #dce775;
  --md-lime-400: #d4e157;
  --md-lime-500: #cddc39;
  --md-lime-600: #c0ca33;
  --md-lime-700: #afb42b;
  --md-lime-800: #9e9d24;
  --md-lime-900: #827717;
  --md-lime-A100: #f4ff81;
  --md-lime-A200: #eeff41;
  --md-lime-A400: #c6ff00;
  --md-lime-A700: #aeea00;

  --md-yellow-50: #fffde7;
  --md-yellow-100: #fff9c4;
  --md-yellow-200: #fff59d;
  --md-yellow-300: #fff176;
  --md-yellow-400: #ffee58;
  --md-yellow-500: #ffeb3b;
  --md-yellow-600: #fdd835;
  --md-yellow-700: #fbc02d;
  --md-yellow-800: #f9a825;
  --md-yellow-900: #f57f17;
  --md-yellow-A100: #ffff8d;
  --md-yellow-A200: #ffff00;
  --md-yellow-A400: #ffea00;
  --md-yellow-A700: #ffd600;

  --md-amber-50: #fff8e1;
  --md-amber-100: #ffecb3;
  --md-amber-200: #ffe082;
  --md-amber-300: #ffd54f;
  --md-amber-400: #ffca28;
  --md-amber-500: #ffc107;
  --md-amber-600: #ffb300;
  --md-amber-700: #ffa000;
  --md-amber-800: #ff8f00;
  --md-amber-900: #ff6f00;
  --md-amber-A100: #ffe57f;
  --md-amber-A200: #ffd740;
  --md-amber-A400: #ffc400;
  --md-amber-A700: #ffab00;

  --md-orange-50: #fff3e0;
  --md-orange-100: #ffe0b2;
  --md-orange-200: #ffcc80;
  --md-orange-300: #ffb74d;
  --md-orange-400: #ffa726;
  --md-orange-500: #ff9800;
  --md-orange-600: #fb8c00;
  --md-orange-700: #f57c00;
  --md-orange-800: #ef6c00;
  --md-orange-900: #e65100;
  --md-orange-A100: #ffd180;
  --md-orange-A200: #ffab40;
  --md-orange-A400: #ff9100;
  --md-orange-A700: #ff6d00;

  --md-deep-orange-50: #fbe9e7;
  --md-deep-orange-100: #ffccbc;
  --md-deep-orange-200: #ffab91;
  --md-deep-orange-300: #ff8a65;
  --md-deep-orange-400: #ff7043;
  --md-deep-orange-500: #ff5722;
  --md-deep-orange-600: #f4511e;
  --md-deep-orange-700: #e64a19;
  --md-deep-orange-800: #d84315;
  --md-deep-orange-900: #bf360c;
  --md-deep-orange-A100: #ff9e80;
  --md-deep-orange-A200: #ff6e40;
  --md-deep-orange-A400: #ff3d00;
  --md-deep-orange-A700: #dd2c00;

  --md-brown-50: #efebe9;
  --md-brown-100: #d7ccc8;
  --md-brown-200: #bcaaa4;
  --md-brown-300: #a1887f;
  --md-brown-400: #8d6e63;
  --md-brown-500: #795548;
  --md-brown-600: #6d4c41;
  --md-brown-700: #5d4037;
  --md-brown-800: #4e342e;
  --md-brown-900: #3e2723;

  --md-grey-50: #fafafa;
  --md-grey-100: #f5f5f5;
  --md-grey-200: #eeeeee;
  --md-grey-300: #e0e0e0;
  --md-grey-400: #bdbdbd;
  --md-grey-500: #9e9e9e;
  --md-grey-600: #757575;
  --md-grey-700: #616161;
  --md-grey-800: #424242;
  --md-grey-900: #212121;

  --md-blue-grey-50: #eceff1;
  --md-blue-grey-100: #cfd8dc;
  --md-blue-grey-200: #b0bec5;
  --md-blue-grey-300: #90a4ae;
  --md-blue-grey-400: #78909c;
  --md-blue-grey-500: #607d8b;
  --md-blue-grey-600: #546e7a;
  --md-blue-grey-700: #455a64;
  --md-blue-grey-800: #37474f;
  --md-blue-grey-900: #263238;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2017, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-Spinner {
  position: absolute;
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 10;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background: var(--jp-layout-color0);
  outline: none;
}

.jp-SpinnerContent {
  font-size: 10px;
  margin: 50px auto;
  text-indent: -9999em;
  width: 3em;
  height: 3em;
  border-radius: 50%;
  background: var(--jp-brand-color3);
  background: linear-gradient(
    to right,
    #f37626 10%,
    rgba(255, 255, 255, 0) 42%
  );
  position: relative;
  animation: load3 1s infinite linear, fadeIn 1s;
}

.jp-SpinnerContent:before {
  width: 50%;
  height: 50%;
  background: #f37626;
  border-radius: 100% 0 0 0;
  position: absolute;
  top: 0;
  left: 0;
  content: '';
}

.jp-SpinnerContent:after {
  background: var(--jp-layout-color0);
  width: 75%;
  height: 75%;
  border-radius: 50%;
  content: '';
  margin: auto;
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
}

@keyframes fadeIn {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}

@keyframes load3 {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

button.jp-mod-styled {
  font-size: var(--jp-ui-font-size1);
  color: var(--jp-ui-font-color0);
  border: none;
  box-sizing: border-box;
  text-align: center;
  line-height: 32px;
  height: 32px;
  padding: 0px 12px;
  letter-spacing: 0.8px;
  outline: none;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
}

input.jp-mod-styled {
  background: var(--jp-input-background);
  height: 28px;
  box-sizing: border-box;
  border: var(--jp-border-width) solid var(--jp-border-color1);
  padding-left: 7px;
  padding-right: 7px;
  font-size: var(--jp-ui-font-size2);
  color: var(--jp-ui-font-color0);
  outline: none;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
}

input[type='checkbox'].jp-mod-styled {
  appearance: checkbox;
  -webkit-appearance: checkbox;
  -moz-appearance: checkbox;
  height: auto;
}

input.jp-mod-styled:focus {
  border: var(--jp-border-width) solid var(--md-blue-500);
  box-shadow: inset 0 0 4px var(--md-blue-300);
}

.jp-FileDialog-Checkbox {
  margin-top: 35px;
  display: flex;
  flex-direction: row;
  align-items: end;
  width: 100%;
}

.jp-FileDialog-Checkbox > label {
  flex: 1 1 auto;
}

.jp-select-wrapper {
  display: flex;
  position: relative;
  flex-direction: column;
  padding: 1px;
  background-color: var(--jp-layout-color1);
  height: 28px;
  box-sizing: border-box;
  margin-bottom: 12px;
}

.jp-select-wrapper.jp-mod-focused select.jp-mod-styled {
  border: var(--jp-border-width) solid var(--jp-input-active-border-color);
  box-shadow: var(--jp-input-box-shadow);
  background-color: var(--jp-input-active-background);
}

select.jp-mod-styled:hover {
  background-color: var(--jp-layout-color1);
  cursor: pointer;
  color: var(--jp-ui-font-color0);
  background-color: var(--jp-input-hover-background);
  box-shadow: inset 0 0px 1px rgba(0, 0, 0, 0.5);
}

select.jp-mod-styled {
  flex: 1 1 auto;
  height: 32px;
  width: 100%;
  font-size: var(--jp-ui-font-size2);
  background: var(--jp-input-background);
  color: var(--jp-ui-font-color0);
  padding: 0 25px 0 8px;
  border: var(--jp-border-width) solid var(--jp-input-border-color);
  border-radius: 0px;
  outline: none;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2016, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

:root {
  --jp-private-toolbar-height: calc(
    28px + var(--jp-border-width)
  ); /* leave 28px for content */
}

.jp-Toolbar {
  color: var(--jp-ui-font-color1);
  flex: 0 0 auto;
  display: flex;
  flex-direction: row;
  border-bottom: var(--jp-border-width) solid var(--jp-toolbar-border-color);
  box-shadow: var(--jp-toolbar-box-shadow);
  background: var(--jp-toolbar-background);
  min-height: var(--jp-toolbar-micro-height);
  padding: 2px;
  z-index: 1;
  overflow-x: auto;
}

/* Toolbar items */

.jp-Toolbar > .jp-Toolbar-item.jp-Toolbar-spacer {
  flex-grow: 1;
  flex-shrink: 1;
}

.jp-Toolbar-item.jp-Toolbar-kernelStatus {
  display: inline-block;
  width: 32px;
  background-repeat: no-repeat;
  background-position: center;
  background-size: 16px;
}

.jp-Toolbar > .jp-Toolbar-item {
  flex: 0 0 auto;
  display: flex;
  padding-left: 1px;
  padding-right: 1px;
  font-size: var(--jp-ui-font-size1);
  line-height: var(--jp-private-toolbar-height);
  height: 100%;
}

/* Toolbar buttons */

/* This is the div we use to wrap the react component into a Widget */
div.jp-ToolbarButton {
  color: transparent;
  border: none;
  box-sizing: border-box;
  outline: none;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
  padding: 0px;
  margin: 0px;
}

button.jp-ToolbarButtonComponent {
  background: var(--jp-layout-color1);
  border: none;
  box-sizing: border-box;
  outline: none;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
  padding: 0px 6px;
  margin: 0px;
  height: 24px;
  border-radius: var(--jp-border-radius);
  display: flex;
  align-items: center;
  text-align: center;
  font-size: 14px;
  min-width: unset;
  min-height: unset;
}

button.jp-ToolbarButtonComponent:disabled {
  opacity: 0.4;
}

button.jp-ToolbarButtonComponent span {
  padding: 0px;
  flex: 0 0 auto;
}

button.jp-ToolbarButtonComponent .jp-ToolbarButtonComponent-label {
  font-size: var(--jp-ui-font-size1);
  line-height: 100%;
  padding-left: 2px;
  color: var(--jp-ui-font-color1);
}

#jp-main-dock-panel[data-mode='single-document']
  .jp-MainAreaWidget
  > .jp-Toolbar.jp-Toolbar-micro {
  padding: 0;
  min-height: 0;
}

#jp-main-dock-panel[data-mode='single-document']
  .jp-MainAreaWidget
  > .jp-Toolbar {
  border: none;
  box-shadow: none;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2017, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Copyright (c) 2014-2017, PhosphorJS Contributors
|
| Distributed under the terms of the BSD 3-Clause License.
|
| The full license is in the file LICENSE, distributed with this software.
|----------------------------------------------------------------------------*/


/* <DEPRECATED> */ body.p-mod-override-cursor *, /* </DEPRECATED> */
body.lm-mod-override-cursor * {
  cursor: inherit !important;
}

/*-----------------------------------------------------------------------------
| Copyright (c) 2014-2016, Jupyter Development Team.
|
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-JSONEditor {
  display: flex;
  flex-direction: column;
  width: 100%;
}

.jp-JSONEditor-host {
  flex: 1 1 auto;
  border: var(--jp-border-width) solid var(--jp-input-border-color);
  border-radius: 0px;
  background: var(--jp-layout-color0);
  min-height: 50px;
  padding: 1px;
}

.jp-JSONEditor.jp-mod-error .jp-JSONEditor-host {
  border-color: red;
  outline-color: red;
}

.jp-JSONEditor-header {
  display: flex;
  flex: 1 0 auto;
  padding: 0 0 0 12px;
}

.jp-JSONEditor-header label {
  flex: 0 0 auto;
}

.jp-JSONEditor-commitButton {
  height: 16px;
  width: 16px;
  background-size: 18px;
  background-repeat: no-repeat;
  background-position: center;
}

.jp-JSONEditor-host.jp-mod-focused {
  background-color: var(--jp-input-active-background);
  border: 1px solid var(--jp-input-active-border-color);
  box-shadow: var(--jp-input-box-shadow);
}

.jp-Editor.jp-mod-dropTarget {
  border: var(--jp-border-width) solid var(--jp-input-active-border-color);
  box-shadow: var(--jp-input-box-shadow);
}

/* BASICS */

.CodeMirror {
  /* Set height, width, borders, and global font properties here */
  font-family: monospace;
  height: 300px;
  color: black;
  direction: ltr;
}

/* PADDING */

.CodeMirror-lines {
  padding: 4px 0; /* Vertical padding around content */
}
.CodeMirror pre.CodeMirror-line,
.CodeMirror pre.CodeMirror-line-like {
  padding: 0 4px; /* Horizontal padding of content */
}

.CodeMirror-scrollbar-filler, .CodeMirror-gutter-filler {
  background-color: white; /* The little square between H and V scrollbars */
}

/* GUTTER */

.CodeMirror-gutters {
  border-right: 1px solid #ddd;
  background-color: #f7f7f7;
  white-space: nowrap;
}
.CodeMirror-linenumbers {}
.CodeMirror-linenumber {
  padding: 0 3px 0 5px;
  min-width: 20px;
  text-align: right;
  color: #999;
  white-space: nowrap;
}

.CodeMirror-guttermarker { color: black; }
.CodeMirror-guttermarker-subtle { color: #999; }

/* CURSOR */

.CodeMirror-cursor {
  border-left: 1px solid black;
  border-right: none;
  width: 0;
}
/* Shown when moving in bi-directional text */
.CodeMirror div.CodeMirror-secondarycursor {
  border-left: 1px solid silver;
}
.cm-fat-cursor .CodeMirror-cursor {
  width: auto;
  border: 0 !important;
  background: #7e7;
}
.cm-fat-cursor div.CodeMirror-cursors {
  z-index: 1;
}
.cm-fat-cursor-mark {
  background-color: rgba(20, 255, 20, 0.5);
  -webkit-animation: blink 1.06s steps(1) infinite;
  -moz-animation: blink 1.06s steps(1) infinite;
  animation: blink 1.06s steps(1) infinite;
}
.cm-animate-fat-cursor {
  width: auto;
  border: 0;
  -webkit-animation: blink 1.06s steps(1) infinite;
  -moz-animation: blink 1.06s steps(1) infinite;
  animation: blink 1.06s steps(1) infinite;
  background-color: #7e7;
}
@-moz-keyframes blink {
  0% {}
  50% { background-color: transparent; }
  100% {}
}
@-webkit-keyframes blink {
  0% {}
  50% { background-color: transparent; }
  100% {}
}
@keyframes blink {
  0% {}
  50% { background-color: transparent; }
  100% {}
}

/* Can style cursor different in overwrite (non-insert) mode */
.CodeMirror-overwrite .CodeMirror-cursor {}

.cm-tab { display: inline-block; text-decoration: inherit; }

.CodeMirror-rulers {
  position: absolute;
  left: 0; right: 0; top: -50px; bottom: 0;
  overflow: hidden;
}
.CodeMirror-ruler {
  border-left: 1px solid #ccc;
  top: 0; bottom: 0;
  position: absolute;
}

/* DEFAULT THEME */

.cm-s-default .cm-header {color: blue;}
.cm-s-default .cm-quote {color: #090;}
.cm-negative {color: #d44;}
.cm-positive {color: #292;}
.cm-header, .cm-strong {font-weight: bold;}
.cm-em {font-style: italic;}
.cm-link {text-decoration: underline;}
.cm-strikethrough {text-decoration: line-through;}

.cm-s-default .cm-keyword {color: #708;}
.cm-s-default .cm-atom {color: #219;}
.cm-s-default .cm-number {color: #164;}
.cm-s-default .cm-def {color: #00f;}
.cm-s-default .cm-variable,
.cm-s-default .cm-punctuation,
.cm-s-default .cm-property,
.cm-s-default .cm-operator {}
.cm-s-default .cm-variable-2 {color: #05a;}
.cm-s-default .cm-variable-3, .cm-s-default .cm-type {color: #085;}
.cm-s-default .cm-comment {color: #a50;}
.cm-s-default .cm-string {color: #a11;}
.cm-s-default .cm-string-2 {color: #f50;}
.cm-s-default .cm-meta {color: #555;}
.cm-s-default .cm-qualifier {color: #555;}
.cm-s-default .cm-builtin {color: #30a;}
.cm-s-default .cm-bracket {color: #997;}
.cm-s-default .cm-tag {color: #170;}
.cm-s-default .cm-attribute {color: #00c;}
.cm-s-default .cm-hr {color: #999;}
.cm-s-default .cm-link {color: #00c;}

.cm-s-default .cm-error {color: #f00;}
.cm-invalidchar {color: #f00;}

.CodeMirror-composing { border-bottom: 2px solid; }

/* Default styles for common addons */

div.CodeMirror span.CodeMirror-matchingbracket {color: #0b0;}
div.CodeMirror span.CodeMirror-nonmatchingbracket {color: #a22;}
.CodeMirror-matchingtag { background: rgba(255, 150, 0, .3); }
.CodeMirror-activeline-background {background: #e8f2ff;}

/* STOP */

/* The rest of this file contains styles related to the mechanics of
   the editor. You probably shouldn't touch them. */

.CodeMirror {
  position: relative;
  overflow: hidden;
  background: white;
}

.CodeMirror-scroll {
  overflow: scroll !important; /* Things will break if this is overridden */
  /* 50px is the magic margin used to hide the element's real scrollbars */
  /* See overflow: hidden in .CodeMirror */
  margin-bottom: -50px; margin-right: -50px;
  padding-bottom: 50px;
  height: 100%;
  outline: none; /* Prevent dragging from highlighting the element */
  position: relative;
}
.CodeMirror-sizer {
  position: relative;
  border-right: 50px solid transparent;
}

/* The fake, visible scrollbars. Used to force redraw during scrolling
   before actual scrolling happens, thus preventing shaking and
   flickering artifacts. */
.CodeMirror-vscrollbar, .CodeMirror-hscrollbar, .CodeMirror-scrollbar-filler, .CodeMirror-gutter-filler {
  position: absolute;
  z-index: 6;
  display: none;
  outline: none;
}
.CodeMirror-vscrollbar {
  right: 0; top: 0;
  overflow-x: hidden;
  overflow-y: scroll;
}
.CodeMirror-hscrollbar {
  bottom: 0; left: 0;
  overflow-y: hidden;
  overflow-x: scroll;
}
.CodeMirror-scrollbar-filler {
  right: 0; bottom: 0;
}
.CodeMirror-gutter-filler {
  left: 0; bottom: 0;
}

.CodeMirror-gutters {
  position: absolute; left: 0; top: 0;
  min-height: 100%;
  z-index: 3;
}
.CodeMirror-gutter {
  white-space: normal;
  height: 100%;
  display: inline-block;
  vertical-align: top;
  margin-bottom: -50px;
}
.CodeMirror-gutter-wrapper {
  position: absolute;
  z-index: 4;
  background: none !important;
  border: none !important;
}
.CodeMirror-gutter-background {
  position: absolute;
  top: 0; bottom: 0;
  z-index: 4;
}
.CodeMirror-gutter-elt {
  position: absolute;
  cursor: default;
  z-index: 4;
}
.CodeMirror-gutter-wrapper ::selection { background-color: transparent }
.CodeMirror-gutter-wrapper ::-moz-selection { background-color: transparent }

.CodeMirror-lines {
  cursor: text;
  min-height: 1px; /* prevents collapsing before first draw */
}
.CodeMirror pre.CodeMirror-line,
.CodeMirror pre.CodeMirror-line-like {
  /* Reset some styles that the rest of the page might have set */
  -moz-border-radius: 0; -webkit-border-radius: 0; border-radius: 0;
  border-width: 0;
  background: transparent;
  font-family: inherit;
  font-size: inherit;
  margin: 0;
  white-space: pre;
  word-wrap: normal;
  line-height: inherit;
  color: inherit;
  z-index: 2;
  position: relative;
  overflow: visible;
  -webkit-tap-highlight-color: transparent;
  -webkit-font-variant-ligatures: contextual;
  font-variant-ligatures: contextual;
}
.CodeMirror-wrap pre.CodeMirror-line,
.CodeMirror-wrap pre.CodeMirror-line-like {
  word-wrap: break-word;
  white-space: pre-wrap;
  word-break: normal;
}

.CodeMirror-linebackground {
  position: absolute;
  left: 0; right: 0; top: 0; bottom: 0;
  z-index: 0;
}

.CodeMirror-linewidget {
  position: relative;
  z-index: 2;
  padding: 0.1px; /* Force widget margins to stay inside of the container */
}

.CodeMirror-widget {}

.CodeMirror-rtl pre { direction: rtl; }

.CodeMirror-code {
  outline: none;
}

/* Force content-box sizing for the elements where we expect it */
.CodeMirror-scroll,
.CodeMirror-sizer,
.CodeMirror-gutter,
.CodeMirror-gutters,
.CodeMirror-linenumber {
  -moz-box-sizing: content-box;
  box-sizing: content-box;
}

.CodeMirror-measure {
  position: absolute;
  width: 100%;
  height: 0;
  overflow: hidden;
  visibility: hidden;
}

.CodeMirror-cursor {
  position: absolute;
  pointer-events: none;
}
.CodeMirror-measure pre { position: static; }

div.CodeMirror-cursors {
  visibility: hidden;
  position: relative;
  z-index: 3;
}
div.CodeMirror-dragcursors {
  visibility: visible;
}

.CodeMirror-focused div.CodeMirror-cursors {
  visibility: visible;
}

.CodeMirror-selected { background: #d9d9d9; }
.CodeMirror-focused .CodeMirror-selected { background: #d7d4f0; }
.CodeMirror-crosshair { cursor: crosshair; }
.CodeMirror-line::selection, .CodeMirror-line > span::selection, .CodeMirror-line > span > span::selection { background: #d7d4f0; }
.CodeMirror-line::-moz-selection, .CodeMirror-line > span::-moz-selection, .CodeMirror-line > span > span::-moz-selection { background: #d7d4f0; }

.cm-searching {
  background-color: #ffa;
  background-color: rgba(255, 255, 0, .4);
}

/* Used to force a border model for a node */
.cm-force-border { padding-right: .1px; }

@media print {
  /* Hide the cursor when printing */
  .CodeMirror div.CodeMirror-cursors {
    visibility: hidden;
  }
}

/* See issue #2901 */
.cm-tab-wrap-hack:after { content: ''; }

/* Help users use markselection to safely style text background */
span.CodeMirror-selectedtext { background: none; }

.CodeMirror-dialog {
  position: absolute;
  left: 0; right: 0;
  background: inherit;
  z-index: 15;
  padding: .1em .8em;
  overflow: hidden;
  color: inherit;
}

.CodeMirror-dialog-top {
  border-bottom: 1px solid #eee;
  top: 0;
}

.CodeMirror-dialog-bottom {
  border-top: 1px solid #eee;
  bottom: 0;
}

.CodeMirror-dialog input {
  border: none;
  outline: none;
  background: transparent;
  width: 20em;
  color: inherit;
  font-family: monospace;
}

.CodeMirror-dialog button {
  font-size: 70%;
}

.CodeMirror-foldmarker {
  color: blue;
  text-shadow: #b9f 1px 1px 2px, #b9f -1px -1px 2px, #b9f 1px -1px 2px, #b9f -1px 1px 2px;
  font-family: arial;
  line-height: .3;
  cursor: pointer;
}
.CodeMirror-foldgutter {
  width: .7em;
}
.CodeMirror-foldgutter-open,
.CodeMirror-foldgutter-folded {
  cursor: pointer;
}
.CodeMirror-foldgutter-open:after {
  content: "\25BE";
}
.CodeMirror-foldgutter-folded:after {
  content: "\25B8";
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.CodeMirror {
  line-height: var(--jp-code-line-height);
  font-size: var(--jp-code-font-size);
  font-family: var(--jp-code-font-family);
  border: 0;
  border-radius: 0;
  height: auto;
  /* Changed to auto to autogrow */
}

.CodeMirror pre {
  padding: 0 var(--jp-code-padding);
}

.jp-CodeMirrorEditor[data-type='inline'] .CodeMirror-dialog {
  background-color: var(--jp-layout-color0);
  color: var(--jp-content-font-color1);
}

/* This causes https://github.com/jupyter/jupyterlab/issues/522 */
/* May not cause it not because we changed it! */
.CodeMirror-lines {
  padding: var(--jp-code-padding) 0;
}

.CodeMirror-linenumber {
  padding: 0 8px;
}

.jp-CodeMirrorEditor {
  cursor: text;
}

.jp-CodeMirrorEditor[data-type='inline'] .CodeMirror-cursor {
  border-left: var(--jp-code-cursor-width0) solid var(--jp-editor-cursor-color);
}

/* When zoomed out 67% and 33% on a screen of 1440 width x 900 height */
@media screen and (min-width: 2138px) and (max-width: 4319px) {
  .jp-CodeMirrorEditor[data-type='inline'] .CodeMirror-cursor {
    border-left: var(--jp-code-cursor-width1) solid
      var(--jp-editor-cursor-color);
  }
}

/* When zoomed out less than 33% */
@media screen and (min-width: 4320px) {
  .jp-CodeMirrorEditor[data-type='inline'] .CodeMirror-cursor {
    border-left: var(--jp-code-cursor-width2) solid
      var(--jp-editor-cursor-color);
  }
}

.CodeMirror.jp-mod-readOnly .CodeMirror-cursor {
  display: none;
}

.CodeMirror-gutters {
  border-right: 1px solid var(--jp-border-color2);
  background-color: var(--jp-layout-color0);
}

.jp-CollaboratorCursor {
  border-left: 5px solid transparent;
  border-right: 5px solid transparent;
  border-top: none;
  border-bottom: 3px solid;
  background-clip: content-box;
  margin-left: -5px;
  margin-right: -5px;
}

.CodeMirror-selectedtext.cm-searching {
  background-color: var(--jp-search-selected-match-background-color) !important;
  color: var(--jp-search-selected-match-color) !important;
}

.cm-searching {
  background-color: var(
    --jp-search-unselected-match-background-color
  ) !important;
  color: var(--jp-search-unselected-match-color) !important;
}

.CodeMirror-focused .CodeMirror-selected {
  background-color: var(--jp-editor-selected-focused-background);
}

.CodeMirror-selected {
  background-color: var(--jp-editor-selected-background);
}

.jp-CollaboratorCursor-hover {
  position: absolute;
  z-index: 1;
  transform: translateX(-50%);
  color: white;
  border-radius: 3px;
  padding-left: 4px;
  padding-right: 4px;
  padding-top: 1px;
  padding-bottom: 1px;
  text-align: center;
  font-size: var(--jp-ui-font-size1);
  white-space: nowrap;
}

.jp-CodeMirror-ruler {
  border-left: 1px dashed var(--jp-border-color2);
}

/**
 * Here is our jupyter theme for CodeMirror syntax highlighting
 * This is used in our marked.js syntax highlighting and CodeMirror itself
 * The string "jupyter" is set in ../codemirror/widget.DEFAULT_CODEMIRROR_THEME
 * This came from the classic notebook, which came form highlight.js/GitHub
 */

/**
 * CodeMirror themes are handling the background/color in this way. This works
 * fine for CodeMirror editors outside the notebook, but the notebook styles
 * these things differently.
 */
.CodeMirror.cm-s-jupyter {
  background: var(--jp-layout-color0);
  color: var(--jp-content-font-color1);
}

/* In the notebook, we want this styling to be handled by its container */
.jp-CodeConsole .CodeMirror.cm-s-jupyter,
.jp-Notebook .CodeMirror.cm-s-jupyter {
  background: transparent;
}

.cm-s-jupyter .CodeMirror-cursor {
  border-left: var(--jp-code-cursor-width0) solid var(--jp-editor-cursor-color);
}
.cm-s-jupyter span.cm-keyword {
  color: var(--jp-mirror-editor-keyword-color);
  font-weight: bold;
}
.cm-s-jupyter span.cm-atom {
  color: var(--jp-mirror-editor-atom-color);
}
.cm-s-jupyter span.cm-number {
  color: var(--jp-mirror-editor-number-color);
}
.cm-s-jupyter span.cm-def {
  color: var(--jp-mirror-editor-def-color);
}
.cm-s-jupyter span.cm-variable {
  color: var(--jp-mirror-editor-variable-color);
}
.cm-s-jupyter span.cm-variable-2 {
  color: var(--jp-mirror-editor-variable-2-color);
}
.cm-s-jupyter span.cm-variable-3 {
  color: var(--jp-mirror-editor-variable-3-color);
}
.cm-s-jupyter span.cm-punctuation {
  color: var(--jp-mirror-editor-punctuation-color);
}
.cm-s-jupyter span.cm-property {
  color: var(--jp-mirror-editor-property-color);
}
.cm-s-jupyter span.cm-operator {
  color: var(--jp-mirror-editor-operator-color);
  font-weight: bold;
}
.cm-s-jupyter span.cm-comment {
  color: var(--jp-mirror-editor-comment-color);
  font-style: italic;
}
.cm-s-jupyter span.cm-string {
  color: var(--jp-mirror-editor-string-color);
}
.cm-s-jupyter span.cm-string-2 {
  color: var(--jp-mirror-editor-string-2-color);
}
.cm-s-jupyter span.cm-meta {
  color: var(--jp-mirror-editor-meta-color);
}
.cm-s-jupyter span.cm-qualifier {
  color: var(--jp-mirror-editor-qualifier-color);
}
.cm-s-jupyter span.cm-builtin {
  color: var(--jp-mirror-editor-builtin-color);
}
.cm-s-jupyter span.cm-bracket {
  color: var(--jp-mirror-editor-bracket-color);
}
.cm-s-jupyter span.cm-tag {
  color: var(--jp-mirror-editor-tag-color);
}
.cm-s-jupyter span.cm-attribute {
  color: var(--jp-mirror-editor-attribute-color);
}
.cm-s-jupyter span.cm-header {
  color: var(--jp-mirror-editor-header-color);
}
.cm-s-jupyter span.cm-quote {
  color: var(--jp-mirror-editor-quote-color);
}
.cm-s-jupyter span.cm-link {
  color: var(--jp-mirror-editor-link-color);
}
.cm-s-jupyter span.cm-error {
  color: var(--jp-mirror-editor-error-color);
}
.cm-s-jupyter span.cm-hr {
  color: #999;
}

.cm-s-jupyter span.cm-tab {
  background: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADAAAAAMCAYAAAAkuj5RAAAAAXNSR0IArs4c6QAAAGFJREFUSMft1LsRQFAQheHPowAKoACx3IgEKtaEHujDjORSgWTH/ZOdnZOcM/sgk/kFFWY0qV8foQwS4MKBCS3qR6ixBJvElOobYAtivseIE120FaowJPN75GMu8j/LfMwNjh4HUpwg4LUAAAAASUVORK5CYII=);
  background-position: right;
  background-repeat: no-repeat;
}

.cm-s-jupyter .CodeMirror-activeline-background,
.cm-s-jupyter .CodeMirror-gutter {
  background-color: var(--jp-layout-color2);
}

/* Styles for shared cursors (remote cursor locations and selected ranges) */
.jp-CodeMirrorEditor .remote-caret {
  position: relative;
  border-left: 2px solid black;
  margin-left: -1px;
  margin-right: -1px;
  box-sizing: border-box;
}

.jp-CodeMirrorEditor .remote-caret > div {
  white-space: nowrap;
  position: absolute;
  top: -1.15em;
  padding-bottom: 0.05em;
  left: -2px;
  font-size: 0.95em;
  background-color: rgb(250, 129, 0);
  font-family: var(--jp-ui-font-family);
  font-weight: bold;
  line-height: normal;
  user-select: none;
  color: white;
  padding-left: 2px;
  padding-right: 2px;
  z-index: 3;
  transition: opacity 0.3s ease-in-out;
}

.jp-CodeMirrorEditor .remote-caret.hide-name > div {
  transition-delay: 0.7s;
  opacity: 0;
}

.jp-CodeMirrorEditor .remote-caret:hover > div {
  opacity: 1;
  transition-delay: 0s;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| RenderedText
|----------------------------------------------------------------------------*/

:root {
  /* This is the padding value to fill the gaps between lines containing spans with background color. */
  --jp-private-code-span-padding: calc(
    (var(--jp-code-line-height) - 1) * var(--jp-code-font-size) / 2
  );
}

.jp-RenderedText {
  text-align: left;
  padding-left: var(--jp-code-padding);
  line-height: var(--jp-code-line-height);
  font-family: var(--jp-code-font-family);
}

.jp-RenderedText pre,
.jp-RenderedJavaScript pre,
.jp-RenderedHTMLCommon pre {
  color: var(--jp-content-font-color1);
  font-size: var(--jp-code-font-size);
  border: none;
  margin: 0px;
  padding: 0px;
}

.jp-RenderedText pre a:link {
  text-decoration: none;
  color: var(--jp-content-link-color);
}
.jp-RenderedText pre a:hover {
  text-decoration: underline;
  color: var(--jp-content-link-color);
}
.jp-RenderedText pre a:visited {
  text-decoration: none;
  color: var(--jp-content-link-color);
}

/* console foregrounds and backgrounds */
.jp-RenderedText pre .ansi-black-fg {
  color: #3e424d;
}
.jp-RenderedText pre .ansi-red-fg {
  color: #e75c58;
}
.jp-RenderedText pre .ansi-green-fg {
  color: #00a250;
}
.jp-RenderedText pre .ansi-yellow-fg {
  color: #ddb62b;
}
.jp-RenderedText pre .ansi-blue-fg {
  color: #208ffb;
}
.jp-RenderedText pre .ansi-magenta-fg {
  color: #d160c4;
}
.jp-RenderedText pre .ansi-cyan-fg {
  color: #60c6c8;
}
.jp-RenderedText pre .ansi-white-fg {
  color: #c5c1b4;
}

.jp-RenderedText pre .ansi-black-bg {
  background-color: #3e424d;
  padding: var(--jp-private-code-span-padding) 0;
}
.jp-RenderedText pre .ansi-red-bg {
  background-color: #e75c58;
  padding: var(--jp-private-code-span-padding) 0;
}
.jp-RenderedText pre .ansi-green-bg {
  background-color: #00a250;
  padding: var(--jp-private-code-span-padding) 0;
}
.jp-RenderedText pre .ansi-yellow-bg {
  background-color: #ddb62b;
  padding: var(--jp-private-code-span-padding) 0;
}
.jp-RenderedText pre .ansi-blue-bg {
  background-color: #208ffb;
  padding: var(--jp-private-code-span-padding) 0;
}
.jp-RenderedText pre .ansi-magenta-bg {
  background-color: #d160c4;
  padding: var(--jp-private-code-span-padding) 0;
}
.jp-RenderedText pre .ansi-cyan-bg {
  background-color: #60c6c8;
  padding: var(--jp-private-code-span-padding) 0;
}
.jp-RenderedText pre .ansi-white-bg {
  background-color: #c5c1b4;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-black-intense-fg {
  color: #282c36;
}
.jp-RenderedText pre .ansi-red-intense-fg {
  color: #b22b31;
}
.jp-RenderedText pre .ansi-green-intense-fg {
  color: #007427;
}
.jp-RenderedText pre .ansi-yellow-intense-fg {
  color: #b27d12;
}
.jp-RenderedText pre .ansi-blue-intense-fg {
  color: #0065ca;
}
.jp-RenderedText pre .ansi-magenta-intense-fg {
  color: #a03196;
}
.jp-RenderedText pre .ansi-cyan-intense-fg {
  color: #258f8f;
}
.jp-RenderedText pre .ansi-white-intense-fg {
  color: #a1a6b2;
}

.jp-RenderedText pre .ansi-black-intense-bg {
  background-color: #282c36;
  padding: var(--jp-private-code-span-padding) 0;
}
.jp-RenderedText pre .ansi-red-intense-bg {
  background-color: #b22b31;
  padding: var(--jp-private-code-span-padding) 0;
}
.jp-RenderedText pre .ansi-green-intense-bg {
  background-color: #007427;
  padding: var(--jp-private-code-span-padding) 0;
}
.jp-RenderedText pre .ansi-yellow-intense-bg {
  background-color: #b27d12;
  padding: var(--jp-private-code-span-padding) 0;
}
.jp-RenderedText pre .ansi-blue-intense-bg {
  background-color: #0065ca;
  padding: var(--jp-private-code-span-padding) 0;
}
.jp-RenderedText pre .ansi-magenta-intense-bg {
  background-color: #a03196;
  padding: var(--jp-private-code-span-padding) 0;
}
.jp-RenderedText pre .ansi-cyan-intense-bg {
  background-color: #258f8f;
  padding: var(--jp-private-code-span-padding) 0;
}
.jp-RenderedText pre .ansi-white-intense-bg {
  background-color: #a1a6b2;
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-default-inverse-fg {
  color: var(--jp-ui-inverse-font-color0);
}
.jp-RenderedText pre .ansi-default-inverse-bg {
  background-color: var(--jp-inverse-layout-color0);
  padding: var(--jp-private-code-span-padding) 0;
}

.jp-RenderedText pre .ansi-bold {
  font-weight: bold;
}
.jp-RenderedText pre .ansi-underline {
  text-decoration: underline;
}

.jp-RenderedText[data-mime-type='application/vnd.jupyter.stderr'] {
  background: var(--jp-rendermime-error-background);
  padding-top: var(--jp-code-padding);
}

/*-----------------------------------------------------------------------------
| RenderedLatex
|----------------------------------------------------------------------------*/

.jp-RenderedLatex {
  color: var(--jp-content-font-color1);
  font-size: var(--jp-content-font-size1);
  line-height: var(--jp-content-line-height);
}

/* Left-justify outputs.*/
.jp-OutputArea-output.jp-RenderedLatex {
  padding: var(--jp-code-padding);
  text-align: left;
}

/*-----------------------------------------------------------------------------
| RenderedHTML
|----------------------------------------------------------------------------*/

.jp-RenderedHTMLCommon {
  color: var(--jp-content-font-color1);
  font-family: var(--jp-content-font-family);
  font-size: var(--jp-content-font-size1);
  line-height: var(--jp-content-line-height);
  /* Give a bit more R padding on Markdown text to keep line lengths reasonable */
  padding-right: 20px;
}

.jp-RenderedHTMLCommon em {
  font-style: italic;
}

.jp-RenderedHTMLCommon strong {
  font-weight: bold;
}

.jp-RenderedHTMLCommon u {
  text-decoration: underline;
}

.jp-RenderedHTMLCommon a:link {
  text-decoration: none;
  color: var(--jp-content-link-color);
}

.jp-RenderedHTMLCommon a:hover {
  text-decoration: underline;
  color: var(--jp-content-link-color);
}

.jp-RenderedHTMLCommon a:visited {
  text-decoration: none;
  color: var(--jp-content-link-color);
}

/* Headings */

.jp-RenderedHTMLCommon h1,
.jp-RenderedHTMLCommon h2,
.jp-RenderedHTMLCommon h3,
.jp-RenderedHTMLCommon h4,
.jp-RenderedHTMLCommon h5,
.jp-RenderedHTMLCommon h6 {
  line-height: var(--jp-content-heading-line-height);
  font-weight: var(--jp-content-heading-font-weight);
  font-style: normal;
  margin: var(--jp-content-heading-margin-top) 0
    var(--jp-content-heading-margin-bottom) 0;
}

.jp-RenderedHTMLCommon h1:first-child,
.jp-RenderedHTMLCommon h2:first-child,
.jp-RenderedHTMLCommon h3:first-child,
.jp-RenderedHTMLCommon h4:first-child,
.jp-RenderedHTMLCommon h5:first-child,
.jp-RenderedHTMLCommon h6:first-child {
  margin-top: calc(0.5 * var(--jp-content-heading-margin-top));
}

.jp-RenderedHTMLCommon h1:last-child,
.jp-RenderedHTMLCommon h2:last-child,
.jp-RenderedHTMLCommon h3:last-child,
.jp-RenderedHTMLCommon h4:last-child,
.jp-RenderedHTMLCommon h5:last-child,
.jp-RenderedHTMLCommon h6:last-child {
  margin-bottom: calc(0.5 * var(--jp-content-heading-margin-bottom));
}

.jp-RenderedHTMLCommon h1 {
  font-size: var(--jp-content-font-size5);
}

.jp-RenderedHTMLCommon h2 {
  font-size: var(--jp-content-font-size4);
}

.jp-RenderedHTMLCommon h3 {
  font-size: var(--jp-content-font-size3);
}

.jp-RenderedHTMLCommon h4 {
  font-size: var(--jp-content-font-size2);
}

.jp-RenderedHTMLCommon h5 {
  font-size: var(--jp-content-font-size1);
}

.jp-RenderedHTMLCommon h6 {
  font-size: var(--jp-content-font-size0);
}

/* Lists */

.jp-RenderedHTMLCommon ul:not(.list-inline),
.jp-RenderedHTMLCommon ol:not(.list-inline) {
  padding-left: 2em;
}

.jp-RenderedHTMLCommon ul {
  list-style: disc;
}

.jp-RenderedHTMLCommon ul ul {
  list-style: square;
}

.jp-RenderedHTMLCommon ul ul ul {
  list-style: circle;
}

.jp-RenderedHTMLCommon ol {
  list-style: decimal;
}

.jp-RenderedHTMLCommon ol ol {
  list-style: upper-alpha;
}

.jp-RenderedHTMLCommon ol ol ol {
  list-style: lower-alpha;
}

.jp-RenderedHTMLCommon ol ol ol ol {
  list-style: lower-roman;
}

.jp-RenderedHTMLCommon ol ol ol ol ol {
  list-style: decimal;
}

.jp-RenderedHTMLCommon ol,
.jp-RenderedHTMLCommon ul {
  margin-bottom: 1em;
}

.jp-RenderedHTMLCommon ul ul,
.jp-RenderedHTMLCommon ul ol,
.jp-RenderedHTMLCommon ol ul,
.jp-RenderedHTMLCommon ol ol {
  margin-bottom: 0em;
}

.jp-RenderedHTMLCommon hr {
  color: var(--jp-border-color2);
  background-color: var(--jp-border-color1);
  margin-top: 1em;
  margin-bottom: 1em;
}

.jp-RenderedHTMLCommon > pre {
  margin: 1.5em 2em;
}

.jp-RenderedHTMLCommon pre,
.jp-RenderedHTMLCommon code {
  border: 0;
  background-color: var(--jp-layout-color0);
  color: var(--jp-content-font-color1);
  font-family: var(--jp-code-font-family);
  font-size: inherit;
  line-height: var(--jp-code-line-height);
  padding: 0;
  white-space: pre-wrap;
}

.jp-RenderedHTMLCommon :not(pre) > code {
  background-color: var(--jp-layout-color2);
  padding: 1px 5px;
}

/* Tables */

.jp-RenderedHTMLCommon table {
  border-collapse: collapse;
  border-spacing: 0;
  border: none;
  color: var(--jp-ui-font-color1);
  font-size: 12px;
  table-layout: fixed;
  margin-left: auto;
  margin-right: auto;
}

.jp-RenderedHTMLCommon thead {
  border-bottom: var(--jp-border-width) solid var(--jp-border-color1);
  vertical-align: bottom;
}

.jp-RenderedHTMLCommon td,
.jp-RenderedHTMLCommon th,
.jp-RenderedHTMLCommon tr {
  vertical-align: middle;
  padding: 0.5em 0.5em;
  line-height: normal;
  white-space: normal;
  max-width: none;
  border: none;
}

.jp-RenderedMarkdown.jp-RenderedHTMLCommon td,
.jp-RenderedMarkdown.jp-RenderedHTMLCommon th {
  max-width: none;
}

:not(.jp-RenderedMarkdown).jp-RenderedHTMLCommon td,
:not(.jp-RenderedMarkdown).jp-RenderedHTMLCommon th,
:not(.jp-RenderedMarkdown).jp-RenderedHTMLCommon tr {
  text-align: right;
}

.jp-RenderedHTMLCommon th {
  font-weight: bold;
}

.jp-RenderedHTMLCommon tbody tr:nth-child(odd) {
  background: var(--jp-layout-color0);
}

.jp-RenderedHTMLCommon tbody tr:nth-child(even) {
  background: var(--jp-rendermime-table-row-background);
}

.jp-RenderedHTMLCommon tbody tr:hover {
  background: var(--jp-rendermime-table-row-hover-background);
}

.jp-RenderedHTMLCommon table {
  margin-bottom: 1em;
}

.jp-RenderedHTMLCommon p {
  text-align: left;
  margin: 0px;
}

.jp-RenderedHTMLCommon p {
  margin-bottom: 1em;
}

.jp-RenderedHTMLCommon img {
  -moz-force-broken-image-icon: 1;
}

/* Restrict to direct children as other images could be nested in other content. */
.jp-RenderedHTMLCommon > img {
  display: block;
  margin-left: 0;
  margin-right: 0;
  margin-bottom: 1em;
}

/* Change color behind transparent images if they need it... */
[data-jp-theme-light='false'] .jp-RenderedImage img.jp-needs-light-background {
  background-color: var(--jp-inverse-layout-color1);
}
[data-jp-theme-light='true'] .jp-RenderedImage img.jp-needs-dark-background {
  background-color: var(--jp-inverse-layout-color1);
}
/* ...or leave it untouched if they don't */
[data-jp-theme-light='false'] .jp-RenderedImage img.jp-needs-dark-background {
}
[data-jp-theme-light='true'] .jp-RenderedImage img.jp-needs-light-background {
}

.jp-RenderedHTMLCommon img,
.jp-RenderedImage img,
.jp-RenderedHTMLCommon svg,
.jp-RenderedSVG svg {
  max-width: 100%;
  height: auto;
}

.jp-RenderedHTMLCommon img.jp-mod-unconfined,
.jp-RenderedImage img.jp-mod-unconfined,
.jp-RenderedHTMLCommon svg.jp-mod-unconfined,
.jp-RenderedSVG svg.jp-mod-unconfined {
  max-width: none;
}

.jp-RenderedHTMLCommon .alert {
  padding: var(--jp-notebook-padding);
  border: var(--jp-border-width) solid transparent;
  border-radius: var(--jp-border-radius);
  margin-bottom: 1em;
}

.jp-RenderedHTMLCommon .alert-info {
  color: var(--jp-info-color0);
  background-color: var(--jp-info-color3);
  border-color: var(--jp-info-color2);
}
.jp-RenderedHTMLCommon .alert-info hr {
  border-color: var(--jp-info-color3);
}
.jp-RenderedHTMLCommon .alert-info > p:last-child,
.jp-RenderedHTMLCommon .alert-info > ul:last-child {
  margin-bottom: 0;
}

.jp-RenderedHTMLCommon .alert-warning {
  color: var(--jp-warn-color0);
  background-color: var(--jp-warn-color3);
  border-color: var(--jp-warn-color2);
}
.jp-RenderedHTMLCommon .alert-warning hr {
  border-color: var(--jp-warn-color3);
}
.jp-RenderedHTMLCommon .alert-warning > p:last-child,
.jp-RenderedHTMLCommon .alert-warning > ul:last-child {
  margin-bottom: 0;
}

.jp-RenderedHTMLCommon .alert-success {
  color: var(--jp-success-color0);
  background-color: var(--jp-success-color3);
  border-color: var(--jp-success-color2);
}
.jp-RenderedHTMLCommon .alert-success hr {
  border-color: var(--jp-success-color3);
}
.jp-RenderedHTMLCommon .alert-success > p:last-child,
.jp-RenderedHTMLCommon .alert-success > ul:last-child {
  margin-bottom: 0;
}

.jp-RenderedHTMLCommon .alert-danger {
  color: var(--jp-error-color0);
  background-color: var(--jp-error-color3);
  border-color: var(--jp-error-color2);
}
.jp-RenderedHTMLCommon .alert-danger hr {
  border-color: var(--jp-error-color3);
}
.jp-RenderedHTMLCommon .alert-danger > p:last-child,
.jp-RenderedHTMLCommon .alert-danger > ul:last-child {
  margin-bottom: 0;
}

.jp-RenderedHTMLCommon blockquote {
  margin: 1em 2em;
  padding: 0 1em;
  border-left: 5px solid var(--jp-border-color2);
}

a.jp-InternalAnchorLink {
  visibility: hidden;
  margin-left: 8px;
  color: var(--md-blue-800);
}

h1:hover .jp-InternalAnchorLink,
h2:hover .jp-InternalAnchorLink,
h3:hover .jp-InternalAnchorLink,
h4:hover .jp-InternalAnchorLink,
h5:hover .jp-InternalAnchorLink,
h6:hover .jp-InternalAnchorLink {
  visibility: visible;
}

.jp-RenderedHTMLCommon kbd {
  background-color: var(--jp-rendermime-table-row-background);
  border: 1px solid var(--jp-border-color0);
  border-bottom-color: var(--jp-border-color2);
  border-radius: 3px;
  box-shadow: inset 0 -1px 0 rgba(0, 0, 0, 0.25);
  display: inline-block;
  font-size: 0.8em;
  line-height: 1em;
  padding: 0.2em 0.5em;
}

/* Most direct children of .jp-RenderedHTMLCommon have a margin-bottom of 1.0.
 * At the bottom of cells this is a bit too much as there is also spacing
 * between cells. Going all the way to 0 gets too tight between markdown and
 * code cells.
 */
.jp-RenderedHTMLCommon > *:last-child {
  margin-bottom: 0.5em;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-MimeDocument {
  outline: none;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Variables
|----------------------------------------------------------------------------*/

:root {
  --jp-private-filebrowser-button-height: 28px;
  --jp-private-filebrowser-button-width: 48px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-FileBrowser {
  display: flex;
  flex-direction: column;
  color: var(--jp-ui-font-color1);
  background: var(--jp-layout-color1);
  /* This is needed so that all font sizing of children done in ems is
   * relative to this base size */
  font-size: var(--jp-ui-font-size1);
}

.jp-FileBrowser-toolbar.jp-Toolbar {
  border-bottom: none;
  height: auto;
  margin: var(--jp-toolbar-header-margin);
  box-shadow: none;
}

.jp-BreadCrumbs {
  flex: 0 0 auto;
  margin: 8px 12px 8px 12px;
}

.jp-BreadCrumbs-item {
  margin: 0px 2px;
  padding: 0px 2px;
  border-radius: var(--jp-border-radius);
  cursor: pointer;
}

.jp-BreadCrumbs-item:hover {
  background-color: var(--jp-layout-color2);
}

.jp-BreadCrumbs-item:first-child {
  margin-left: 0px;
}

.jp-BreadCrumbs-item.jp-mod-dropTarget {
  background-color: var(--jp-brand-color2);
  opacity: 0.7;
}

/*-----------------------------------------------------------------------------
| Buttons
|----------------------------------------------------------------------------*/

.jp-FileBrowser-toolbar.jp-Toolbar {
  padding: 0px;
  margin: 8px 12px 0px 12px;
}

.jp-FileBrowser-toolbar.jp-Toolbar {
  justify-content: flex-start;
}

.jp-FileBrowser-toolbar.jp-Toolbar .jp-Toolbar-item {
  flex: 0 0 auto;
  padding-left: 0px;
  padding-right: 2px;
}

.jp-FileBrowser-toolbar.jp-Toolbar .jp-ToolbarButtonComponent {
  width: 40px;
}

.jp-FileBrowser-toolbar.jp-Toolbar
  .jp-Toolbar-item:first-child
  .jp-ToolbarButtonComponent {
  width: 72px;
  background: var(--jp-brand-color1);
}

.jp-FileBrowser-toolbar.jp-Toolbar
  .jp-Toolbar-item:first-child
  .jp-ToolbarButtonComponent:focus-visible {
  background-color: var(--jp-brand-color0);
}

.jp-FileBrowser-toolbar.jp-Toolbar
  .jp-Toolbar-item:first-child
  .jp-ToolbarButtonComponent
  .jp-icon3 {
  fill: white;
}

/*-----------------------------------------------------------------------------
| Other styles
|----------------------------------------------------------------------------*/

.jp-FileDialog.jp-mod-conflict input {
  color: var(--jp-error-color1);
}

.jp-FileDialog .jp-new-name-title {
  margin-top: 12px;
}

.jp-LastModified-hidden {
  display: none;
}

.jp-FileBrowser-filterBox {
  padding: 0px;
  flex: 0 0 auto;
  margin: 8px 12px 0px 12px;
}

/*-----------------------------------------------------------------------------
| DirListing
|----------------------------------------------------------------------------*/

.jp-DirListing {
  flex: 1 1 auto;
  display: flex;
  flex-direction: column;
  outline: 0;
}

.jp-DirListing:focus-visible {
  border: 1px solid var(--jp-brand-color1);
}

.jp-DirListing-header {
  flex: 0 0 auto;
  display: flex;
  flex-direction: row;
  overflow: hidden;
  border-top: var(--jp-border-width) solid var(--jp-border-color2);
  border-bottom: var(--jp-border-width) solid var(--jp-border-color1);
  box-shadow: var(--jp-toolbar-box-shadow);
  z-index: 2;
}

.jp-DirListing-headerItem {
  padding: 4px 12px 2px 12px;
  font-weight: 500;
}

.jp-DirListing-headerItem:hover {
  background: var(--jp-layout-color2);
}

.jp-DirListing-headerItem.jp-id-name {
  flex: 1 0 84px;
}

.jp-DirListing-headerItem.jp-id-modified {
  flex: 0 0 112px;
  border-left: var(--jp-border-width) solid var(--jp-border-color2);
  text-align: right;
}

.jp-id-narrow {
  display: none;
  flex: 0 0 5px;
  padding: 4px 4px;
  border-left: var(--jp-border-width) solid var(--jp-border-color2);
  text-align: right;
  color: var(--jp-border-color2);
}

.jp-DirListing-narrow .jp-id-narrow {
  display: block;
}

.jp-DirListing-narrow .jp-id-modified,
.jp-DirListing-narrow .jp-DirListing-itemModified {
  display: none;
}

.jp-DirListing-headerItem.jp-mod-selected {
  font-weight: 600;
}

/* increase specificity to override bundled default */
.jp-DirListing-content {
  flex: 1 1 auto;
  margin: 0;
  padding: 0;
  list-style-type: none;
  overflow: auto;
  background-color: var(--jp-layout-color1);
}

.jp-DirListing-content mark {
  color: var(--jp-ui-font-color0);
  background-color: transparent;
  font-weight: bold;
}

.jp-DirListing-content .jp-DirListing-item.jp-mod-selected mark {
  color: var(--jp-ui-inverse-font-color0);
}

/* Style the directory listing content when a user drops a file to upload */
.jp-DirListing.jp-mod-native-drop .jp-DirListing-content {
  outline: 5px dashed rgba(128, 128, 128, 0.5);
  outline-offset: -10px;
  cursor: copy;
}

.jp-DirListing-item {
  display: flex;
  flex-direction: row;
  padding: 4px 12px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.jp-DirListing-item[data-is-dot] {
  opacity: 75%;
}

.jp-DirListing-item.jp-mod-selected {
  color: var(--jp-ui-inverse-font-color1);
  background: var(--jp-brand-color1);
}

.jp-DirListing-item.jp-mod-dropTarget {
  background: var(--jp-brand-color3);
}

.jp-DirListing-item:hover:not(.jp-mod-selected) {
  background: var(--jp-layout-color2);
}

.jp-DirListing-itemIcon {
  flex: 0 0 20px;
  margin-right: 4px;
}

.jp-DirListing-itemText {
  flex: 1 0 64px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  user-select: none;
}

.jp-DirListing-itemModified {
  flex: 0 0 125px;
  text-align: right;
}

.jp-DirListing-editor {
  flex: 1 0 64px;
  outline: none;
  border: none;
}

.jp-DirListing-item.jp-mod-running .jp-DirListing-itemIcon:before {
  color: var(--jp-success-color1);
  content: '\25CF';
  font-size: 8px;
  position: absolute;
  left: -8px;
}

.jp-DirListing-item.jp-mod-running.jp-mod-selected
  .jp-DirListing-itemIcon:before {
  color: var(--jp-ui-inverse-font-color1);
}

.jp-DirListing-item.lm-mod-drag-image,
.jp-DirListing-item.jp-mod-selected.lm-mod-drag-image {
  font-size: var(--jp-ui-font-size1);
  padding-left: 4px;
  margin-left: 4px;
  width: 160px;
  background-color: var(--jp-ui-inverse-font-color2);
  box-shadow: var(--jp-elevation-z2);
  border-radius: 0px;
  color: var(--jp-ui-font-color1);
  transform: translateX(-40%) translateY(-58%);
}

.jp-DirListing-deadSpace {
  flex: 1 1 auto;
  margin: 0;
  padding: 0;
  list-style-type: none;
  overflow: auto;
  background-color: var(--jp-layout-color1);
}

.jp-Document {
  min-width: 120px;
  min-height: 120px;
  outline: none;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Private CSS variables
|----------------------------------------------------------------------------*/

:root {
}

/*-----------------------------------------------------------------------------
| Main OutputArea
| OutputArea has a list of Outputs
|----------------------------------------------------------------------------*/

.jp-OutputArea {
  overflow-y: auto;
}

.jp-OutputArea-child {
  display: flex;
  flex-direction: row;
}

body[data-format='mobile'] .jp-OutputArea-child {
  flex-direction: column;
}

.jp-OutputPrompt {
  flex: 0 0 var(--jp-cell-prompt-width);
  color: var(--jp-cell-outprompt-font-color);
  font-family: var(--jp-cell-prompt-font-family);
  padding: var(--jp-code-padding);
  letter-spacing: var(--jp-cell-prompt-letter-spacing);
  line-height: var(--jp-code-line-height);
  font-size: var(--jp-code-font-size);
  border: var(--jp-border-width) solid transparent;
  opacity: var(--jp-cell-prompt-opacity);
  /* Right align prompt text, don't wrap to handle large prompt numbers */
  text-align: right;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  /* Disable text selection */
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

body[data-format='mobile'] .jp-OutputPrompt {
  flex: 0 0 auto;
  text-align: left;
}

.jp-OutputArea-output {
  height: auto;
  overflow: auto;
  user-select: text;
  -moz-user-select: text;
  -webkit-user-select: text;
  -ms-user-select: text;
}

.jp-OutputArea-child .jp-OutputArea-output {
  flex-grow: 1;
  flex-shrink: 1;
}

body[data-format='mobile'] .jp-OutputArea-child .jp-OutputArea-output {
  margin-left: var(--jp-notebook-padding);
}

/**
 * Isolated output.
 */
.jp-OutputArea-output.jp-mod-isolated {
  width: 100%;
  display: block;
}

/*
When drag events occur, `p-mod-override-cursor` is added to the body.
Because iframes steal all cursor events, the following two rules are necessary
to suppress pointer events while resize drags are occurring. There may be a
better solution to this problem.
*/
body.lm-mod-override-cursor .jp-OutputArea-output.jp-mod-isolated {
  position: relative;
}

body.lm-mod-override-cursor .jp-OutputArea-output.jp-mod-isolated:before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: transparent;
}

/* pre */

.jp-OutputArea-output pre {
  border: none;
  margin: 0px;
  padding: 0px;
  overflow-x: auto;
  overflow-y: auto;
  word-break: break-all;
  word-wrap: break-word;
  white-space: pre-wrap;
}

/* tables */

.jp-OutputArea-output.jp-RenderedHTMLCommon table {
  margin-left: 0;
  margin-right: 0;
}

/* description lists */

.jp-OutputArea-output dl,
.jp-OutputArea-output dt,
.jp-OutputArea-output dd {
  display: block;
}

.jp-OutputArea-output dl {
  width: 100%;
  overflow: hidden;
  padding: 0;
  margin: 0;
}

.jp-OutputArea-output dt {
  font-weight: bold;
  float: left;
  width: 20%;
  padding: 0;
  margin: 0;
}

.jp-OutputArea-output dd {
  float: left;
  width: 80%;
  padding: 0;
  margin: 0;
}

/* Hide the gutter in case of
 *  - nested output areas (e.g. in the case of output widgets)
 *  - mirrored output areas
 */
.jp-OutputArea .jp-OutputArea .jp-OutputArea-prompt {
  display: none;
}

/*-----------------------------------------------------------------------------
| executeResult is added to any Output-result for the display of the object
| returned by a cell
|----------------------------------------------------------------------------*/

.jp-OutputArea-output.jp-OutputArea-executeResult {
  margin-left: 0px;
  flex: 1 1 auto;
}

/* Text output with the Out[] prompt needs a top padding to match the
 * alignment of the Out[] prompt itself.
 */
.jp-OutputArea-executeResult .jp-RenderedText.jp-OutputArea-output {
  padding-top: var(--jp-code-padding);
  border-top: var(--jp-border-width) solid transparent;
}

/*-----------------------------------------------------------------------------
| The Stdin output
|----------------------------------------------------------------------------*/

.jp-OutputArea-stdin {
  line-height: var(--jp-code-line-height);
  padding-top: var(--jp-code-padding);
  display: flex;
}

.jp-Stdin-prompt {
  color: var(--jp-content-font-color0);
  padding-right: var(--jp-code-padding);
  vertical-align: baseline;
  flex: 0 0 auto;
}

.jp-Stdin-input {
  font-family: var(--jp-code-font-family);
  font-size: inherit;
  color: inherit;
  background-color: inherit;
  width: 42%;
  min-width: 200px;
  /* make sure input baseline aligns with prompt */
  vertical-align: baseline;
  /* padding + margin = 0.5em between prompt and cursor */
  padding: 0em 0.25em;
  margin: 0em 0.25em;
  flex: 0 0 70%;
}

.jp-Stdin-input:focus {
  box-shadow: none;
}

/*-----------------------------------------------------------------------------
| Output Area View
|----------------------------------------------------------------------------*/

.jp-LinkedOutputView .jp-OutputArea {
  height: 100%;
  display: block;
}

.jp-LinkedOutputView .jp-OutputArea-output:only-child {
  height: 100%;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

.jp-Collapser {
  flex: 0 0 var(--jp-cell-collapser-width);
  padding: 0px;
  margin: 0px;
  border: none;
  outline: none;
  background: transparent;
  border-radius: var(--jp-border-radius);
  opacity: 1;
}

.jp-Collapser-child {
  display: block;
  width: 100%;
  box-sizing: border-box;
  /* height: 100% doesn't work because the height of its parent is computed from content */
  position: absolute;
  top: 0px;
  bottom: 0px;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Header/Footer
|----------------------------------------------------------------------------*/

/* Hidden by zero height by default */
.jp-CellHeader,
.jp-CellFooter {
  height: 0px;
  width: 100%;
  padding: 0px;
  margin: 0px;
  border: none;
  outline: none;
  background: transparent;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Input
|----------------------------------------------------------------------------*/

/* All input areas */
.jp-InputArea {
  display: flex;
  flex-direction: row;
  overflow: hidden;
}

body[data-format='mobile'] .jp-InputArea {
  flex-direction: column;
}

.jp-InputArea-editor {
  flex: 1 1 auto;
  overflow: hidden;
}

.jp-InputArea-editor {
  /* This is the non-active, default styling */
  border: var(--jp-border-width) solid var(--jp-cell-editor-border-color);
  border-radius: 0px;
  background: var(--jp-cell-editor-background);
}

body[data-format='mobile'] .jp-InputArea-editor {
  margin-left: var(--jp-notebook-padding);
}

.jp-InputPrompt {
  flex: 0 0 var(--jp-cell-prompt-width);
  color: var(--jp-cell-inprompt-font-color);
  font-family: var(--jp-cell-prompt-font-family);
  padding: var(--jp-code-padding);
  letter-spacing: var(--jp-cell-prompt-letter-spacing);
  opacity: var(--jp-cell-prompt-opacity);
  line-height: var(--jp-code-line-height);
  font-size: var(--jp-code-font-size);
  border: var(--jp-border-width) solid transparent;
  opacity: var(--jp-cell-prompt-opacity);
  /* Right align prompt text, don't wrap to handle large prompt numbers */
  text-align: right;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  /* Disable text selection */
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

body[data-format='mobile'] .jp-InputPrompt {
  flex: 0 0 auto;
  text-align: left;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Placeholder
|----------------------------------------------------------------------------*/

.jp-Placeholder {
  display: flex;
  flex-direction: row;
  flex: 1 1 auto;
}

.jp-Placeholder-prompt {
  box-sizing: border-box;
}

.jp-Placeholder-content {
  flex: 1 1 auto;
  border: none;
  background: transparent;
  height: 20px;
  box-sizing: border-box;
}

.jp-Placeholder-content .jp-MoreHorizIcon {
  width: 32px;
  height: 16px;
  border: 1px solid transparent;
  border-radius: var(--jp-border-radius);
}

.jp-Placeholder-content .jp-MoreHorizIcon:hover {
  border: 1px solid var(--jp-border-color1);
  box-shadow: 0px 0px 2px 0px rgba(0, 0, 0, 0.25);
  background-color: var(--jp-layout-color0);
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Private CSS variables
|----------------------------------------------------------------------------*/

:root {
  --jp-private-cell-scrolling-output-offset: 5px;
}

/*-----------------------------------------------------------------------------
| Cell
|----------------------------------------------------------------------------*/

.jp-Cell {
  padding: var(--jp-cell-padding);
  margin: 0px;
  border: none;
  outline: none;
  background: transparent;
}

/*-----------------------------------------------------------------------------
| Common input/output
|----------------------------------------------------------------------------*/

.jp-Cell-inputWrapper,
.jp-Cell-outputWrapper {
  display: flex;
  flex-direction: row;
  padding: 0px;
  margin: 0px;
  /* Added to reveal the box-shadow on the input and output collapsers. */
  overflow: visible;
}

/* Only input/output areas inside cells */
.jp-Cell-inputArea,
.jp-Cell-outputArea {
  flex: 1 1 auto;
}

/*-----------------------------------------------------------------------------
| Collapser
|----------------------------------------------------------------------------*/

/* Make the output collapser disappear when there is not output, but do so
 * in a manner that leaves it in the layout and preserves its width.
 */
.jp-Cell.jp-mod-noOutputs .jp-Cell-outputCollapser {
  border: none !important;
  background: transparent !important;
}

.jp-Cell:not(.jp-mod-noOutputs) .jp-Cell-outputCollapser {
  min-height: var(--jp-cell-collapser-min-height);
}

/*-----------------------------------------------------------------------------
| Output
|----------------------------------------------------------------------------*/

/* Put a space between input and output when there IS output */
.jp-Cell:not(.jp-mod-noOutputs) .jp-Cell-outputWrapper {
  margin-top: 5px;
}

.jp-CodeCell.jp-mod-outputsScrolled .jp-Cell-outputArea {
  overflow-y: auto;
  max-height: 200px;
  box-shadow: inset 0 0 6px 2px rgba(0, 0, 0, 0.3);
  margin-left: var(--jp-private-cell-scrolling-output-offset);
}

.jp-CodeCell.jp-mod-outputsScrolled .jp-OutputArea-prompt {
  flex: 0 0
    calc(
      var(--jp-cell-prompt-width) -
        var(--jp-private-cell-scrolling-output-offset)
    );
}

/*-----------------------------------------------------------------------------
| CodeCell
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| MarkdownCell
|----------------------------------------------------------------------------*/

.jp-MarkdownOutput {
  flex: 1 1 auto;
  margin-top: 0;
  margin-bottom: 0;
  padding-left: var(--jp-code-padding);
}

.jp-MarkdownOutput.jp-RenderedHTMLCommon {
  overflow: auto;
}

.jp-showHiddenCellsButton {
  margin-left: calc(var(--jp-cell-prompt-width) + 2 * var(--jp-code-padding));
  margin-top: var(--jp-code-padding);
  border: 1px solid var(--jp-border-color2);
  background-color: var(--jp-border-color3) !important;
  color: var(--jp-content-font-color0) !important;
}

.jp-showHiddenCellsButton:hover {
  background-color: var(--jp-border-color2) !important;
}

.jp-collapseHeadingButton {
  display: none;
}

.jp-MarkdownCell:hover .jp-collapseHeadingButton {
  display: flex;
  min-height: var(--jp-cell-collapser-min-height);
  position: absolute;
  right: 0;
  top: 0;
  bottom: 0;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Variables
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------

/*-----------------------------------------------------------------------------
| Styles
|----------------------------------------------------------------------------*/

.jp-NotebookPanel-toolbar {
  padding: 2px;
}

.jp-Toolbar-item.jp-Notebook-toolbarCellType .jp-select-wrapper.jp-mod-focused {
  border: none;
  box-shadow: none;
}

.jp-Notebook-toolbarCellTypeDropdown select {
  height: 24px;
  font-size: var(--jp-ui-font-size1);
  line-height: 14px;
  border-radius: 0;
  display: block;
}

.jp-Notebook-toolbarCellTypeDropdown span {
  top: 5px !important;
}

/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Private CSS variables
|----------------------------------------------------------------------------*/

:root {
  --jp-private-notebook-dragImage-width: 304px;
  --jp-private-notebook-dragImage-height: 36px;
  --jp-private-notebook-selected-color: var(--md-blue-400);
  --jp-private-notebook-active-color: var(--md-green-400);
}

/*-----------------------------------------------------------------------------
| Imports
|----------------------------------------------------------------------------*/

/*-----------------------------------------------------------------------------
| Notebook
|----------------------------------------------------------------------------*/

.jp-NotebookPanel {
  display: block;
  height: 100%;
}

.jp-NotebookPanel.jp-Document {
  min-width: 240px;
  min-height: 120px;
}

.jp-Notebook {
  padding: var(--jp-notebook-padding);
  outline: none;
  overflow: auto;
  background: var(--jp-layout-color0);
}

.jp-Notebook.jp-mod-scrollPastEnd::after {
  display: block;
  content: '';
  min-height: var(--jp-notebook-scroll-padding);
}

.jp-MainAreaWidget-ContainStrict .jp-Notebook * {
  contain: strict;
}

.jp-Notebook-render * {
  contain: none !important;
}

.jp-Notebook .jp-Cell {
  overflow: visible;
}

.jp-Notebook .jp-Cell .jp-InputPrompt {
  cursor: move;
  float: left;
}

/*-----------------------------------------------------------------------------
| Notebook state related styling
|
| The notebook and cells each have states, here are the possibilities:
|
| - Notebook
|   - Command
|   - Edit
| - Cell
|   - None
|   - Active (only one can be active)
|   - Selected (the cells actions are applied to)
|   - Multiselected (when multiple selected, the cursor)
|   - No outputs
|----------------------------------------------------------------------------*/

/* Command or edit modes */

.jp-Notebook .jp-Cell:not(.jp-mod-active) .jp-InputPrompt {
  opacity: var(--jp-cell-prompt-not-active-opacity);
  color: var(--jp-cell-prompt-not-active-font-color);
}

.jp-Notebook .jp-Cell:not(.jp-mod-active) .jp-OutputPrompt {
  opacity: var(--jp-cell-prompt-not-active-opacity);
  color: var(--jp-cell-prompt-not-active-font-color);
}

/* cell is active */
.jp-Notebook .jp-Cell.jp-mod-active .jp-Collapser {
  background: var(--jp-brand-color1);
}

/* cell is dirty */
.jp-Notebook .jp-Cell.jp-mod-dirty .jp-InputPrompt {
  color: var(--jp-warn-color1);
}
.jp-Notebook .jp-Cell.jp-mod-dirty .jp-InputPrompt:before {
  color: var(--jp-warn-color1);
  content: '•';
}

.jp-Notebook .jp-Cell.jp-mod-active.jp-mod-dirty .jp-Collapser {
  background: var(--jp-warn-color1);
}

/* collapser is hovered */
.jp-Notebook .jp-Cell .jp-Collapser:hover {
  box-shadow: var(--jp-elevation-z2);
  background: var(--jp-brand-color1);
  opacity: var(--jp-cell-collapser-not-active-hover-opacity);
}

/* cell is active and collapser is hovered */
.jp-Notebook .jp-Cell.jp-mod-active .jp-Collapser:hover {
  background: var(--jp-brand-color0);
  opacity: 1;
}

/* Command mode */

.jp-Notebook.jp-mod-commandMode .jp-Cell.jp-mod-selected {
  background: var(--jp-notebook-multiselected-color);
}

.jp-Notebook.jp-mod-commandMode
  .jp-Cell.jp-mod-active.jp-mod-selected:not(.jp-mod-multiSelected) {
  background: transparent;
}

/* Edit mode */

.jp-Notebook.jp-mod-editMode .jp-Cell.jp-mod-active .jp-InputArea-editor {
  border: var(--jp-border-width) solid var(--jp-cell-editor-active-border-color);
  box-shadow: var(--jp-input-box-shadow);
  background-color: var(--jp-cell-editor-active-background);
}

/*-----------------------------------------------------------------------------
| Notebook drag and drop
|----------------------------------------------------------------------------*/

.jp-Notebook-cell.jp-mod-dropSource {
  opacity: 0.5;
}

.jp-Notebook-cell.jp-mod-dropTarget,
.jp-Notebook.jp-mod-commandMode
  .jp-Notebook-cell.jp-mod-active.jp-mod-selected.jp-mod-dropTarget {
  border-top-color: var(--jp-private-notebook-selected-color);
  border-top-style: solid;
  border-top-width: 2px;
}

.jp-dragImage {
  display: block;
  flex-direction: row;
  width: var(--jp-private-notebook-dragImage-width);
  height: var(--jp-private-notebook-dragImage-height);
  border: var(--jp-border-width) solid var(--jp-cell-editor-border-color);
  background: var(--jp-cell-editor-background);
  overflow: visible;
}

.jp-dragImage-singlePrompt {
  box-shadow: 2px 2px 4px 0px rgba(0, 0, 0, 0.12);
}

.jp-dragImage .jp-dragImage-content {
  flex: 1 1 auto;
  z-index: 2;
  font-size: var(--jp-code-font-size);
  font-family: var(--jp-code-font-family);
  line-height: var(--jp-code-line-height);
  padding: var(--jp-code-padding);
  border: var(--jp-border-width) solid var(--jp-cell-editor-border-color);
  background: var(--jp-cell-editor-background-color);
  color: var(--jp-content-font-color3);
  text-align: left;
  margin: 4px 4px 4px 0px;
}

.jp-dragImage .jp-dragImage-prompt {
  flex: 0 0 auto;
  min-width: 36px;
  color: var(--jp-cell-inprompt-font-color);
  padding: var(--jp-code-padding);
  padding-left: 12px;
  font-family: var(--jp-cell-prompt-font-family);
  letter-spacing: var(--jp-cell-prompt-letter-spacing);
  line-height: 1.9;
  font-size: var(--jp-code-font-size);
  border: var(--jp-border-width) solid transparent;
}

.jp-dragImage-multipleBack {
  z-index: -1;
  position: absolute;
  height: 32px;
  width: 300px;
  top: 8px;
  left: 8px;
  background: var(--jp-layout-color2);
  border: var(--jp-border-width) solid var(--jp-input-border-color);
  box-shadow: 2px 2px 4px 0px rgba(0, 0, 0, 0.12);
}

/*-----------------------------------------------------------------------------
| Cell toolbar
|----------------------------------------------------------------------------*/

.jp-NotebookTools {
  display: block;
  min-width: var(--jp-sidebar-min-width);
  color: var(--jp-ui-font-color1);
  background: var(--jp-layout-color1);
  /* This is needed so that all font sizing of children done in ems is
    * relative to this base size */
  font-size: var(--jp-ui-font-size1);
  overflow: auto;
}

.jp-NotebookTools-tool {
  padding: 0px 12px 0 12px;
}

.jp-ActiveCellTool {
  padding: 12px;
  background-color: var(--jp-layout-color1);
  border-top: none !important;
}

.jp-ActiveCellTool .jp-InputArea-prompt {
  flex: 0 0 auto;
  padding-left: 0px;
}

.jp-ActiveCellTool .jp-InputArea-editor {
  flex: 1 1 auto;
  background: var(--jp-cell-editor-background);
  border-color: var(--jp-cell-editor-border-color);
}

.jp-ActiveCellTool .jp-InputArea-editor .CodeMirror {
  background: transparent;
}

.jp-MetadataEditorTool {
  flex-direction: column;
  padding: 12px 0px 12px 0px;
}

.jp-RankedPanel > :not(:first-child) {
  margin-top: 12px;
}

.jp-KeySelector select.jp-mod-styled {
  font-size: var(--jp-ui-font-size1);
  color: var(--jp-ui-font-color0);
  border: var(--jp-border-width) solid var(--jp-border-color1);
}

.jp-KeySelector label,
.jp-MetadataEditorTool label {
  line-height: 1.4;
}

.jp-NotebookTools .jp-select-wrapper {
  margin-top: 4px;
  margin-bottom: 0px;
}

.jp-NotebookTools .jp-Collapse {
  margin-top: 16px;
}

/*-----------------------------------------------------------------------------
| Presentation Mode (.jp-mod-presentationMode)
|----------------------------------------------------------------------------*/

.jp-mod-presentationMode .jp-Notebook {
  --jp-content-font-size1: var(--jp-content-presentation-font-size1);
  --jp-code-font-size: var(--jp-code-presentation-font-size);
}

.jp-mod-presentationMode .jp-Notebook .jp-Cell .jp-InputPrompt,
.jp-mod-presentationMode .jp-Notebook .jp-Cell .jp-OutputPrompt {
  flex: 0 0 110px;
}

/*-----------------------------------------------------------------------------
| Placeholder
|----------------------------------------------------------------------------*/

.jp-Cell-Placeholder {
  padding-left: 55px;
}

.jp-Cell-Placeholder-wrapper {
  background: #fff;
  border: 1px solid;
  border-color: #e5e6e9 #dfe0e4 #d0d1d5;
  border-radius: 4px;
  -webkit-border-radius: 4px;
  margin: 10px 15px;
}

.jp-Cell-Placeholder-wrapper-inner {
  padding: 15px;
  position: relative;
}

.jp-Cell-Placeholder-wrapper-body {
  background-repeat: repeat;
  background-size: 50% auto;
}

.jp-Cell-Placeholder-wrapper-body div {
  background: #f6f7f8;
  background-image: -webkit-linear-gradient(
    left,
    #f6f7f8 0%,
    #edeef1 20%,
    #f6f7f8 40%,
    #f6f7f8 100%
  );
  background-repeat: no-repeat;
  background-size: 800px 104px;
  height: 104px;
  position: relative;
}

.jp-Cell-Placeholder-wrapper-body div {
  position: absolute;
  right: 15px;
  left: 15px;
  top: 15px;
}

div.jp-Cell-Placeholder-h1 {
  top: 20px;
  height: 20px;
  left: 15px;
  width: 150px;
}

div.jp-Cell-Placeholder-h2 {
  left: 15px;
  top: 50px;
  height: 10px;
  width: 100px;
}

div.jp-Cell-Placeholder-content-1,
div.jp-Cell-Placeholder-content-2,
div.jp-Cell-Placeholder-content-3 {
  left: 15px;
  right: 15px;
  height: 10px;
}

div.jp-Cell-Placeholder-content-1 {
  top: 100px;
}

div.jp-Cell-Placeholder-content-2 {
  top: 120px;
}

div.jp-Cell-Placeholder-content-3 {
  top: 140px;
}

</style>

    <style type="text/css">
/*-----------------------------------------------------------------------------
| Copyright (c) Jupyter Development Team.
| Distributed under the terms of the Modified BSD License.
|----------------------------------------------------------------------------*/

/*
The following CSS variables define the main, public API for styling JupyterLab.
These variables should be used by all plugins wherever possible. In other
words, plugins should not define custom colors, sizes, etc unless absolutely
necessary. This enables users to change the visual theme of JupyterLab
by changing these variables.

Many variables appear in an ordered sequence (0,1,2,3). These sequences
are designed to work well together, so for example, `--jp-border-color1` should
be used with `--jp-layout-color1`. The numbers have the following meanings:

* 0: super-primary, reserved for special emphasis
* 1: primary, most important under normal situations
* 2: secondary, next most important under normal situations
* 3: tertiary, next most important under normal situations

Throughout JupyterLab, we are mostly following principles from Google's
Material Design when selecting colors. We are not, however, following
all of MD as it is not optimized for dense, information rich UIs.
*/

:root {
  /* Elevation
   *
   * We style box-shadows using Material Design's idea of elevation. These particular numbers are taken from here:
   *
   * https://github.com/material-components/material-components-web
   * https://material-components-web.appspot.com/elevation.html
   */

  --jp-shadow-base-lightness: 0;
  --jp-shadow-umbra-color: rgba(
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    0.2
  );
  --jp-shadow-penumbra-color: rgba(
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    0.14
  );
  --jp-shadow-ambient-color: rgba(
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    var(--jp-shadow-base-lightness),
    0.12
  );
  --jp-elevation-z0: none;
  --jp-elevation-z1: 0px 2px 1px -1px var(--jp-shadow-umbra-color),
    0px 1px 1px 0px var(--jp-shadow-penumbra-color),
    0px 1px 3px 0px var(--jp-shadow-ambient-color);
  --jp-elevation-z2: 0px 3px 1px -2px var(--jp-shadow-umbra-color),
    0px 2px 2px 0px var(--jp-shadow-penumbra-color),
    0px 1px 5px 0px var(--jp-shadow-ambient-color);
  --jp-elevation-z4: 0px 2px 4px -1px var(--jp-shadow-umbra-color),
    0px 4px 5px 0px var(--jp-shadow-penumbra-color),
    0px 1px 10px 0px var(--jp-shadow-ambient-color);
  --jp-elevation-z6: 0px 3px 5px -1px var(--jp-shadow-umbra-color),
    0px 6px 10px 0px var(--jp-shadow-penumbra-color),
    0px 1px 18px 0px var(--jp-shadow-ambient-color);
  --jp-elevation-z8: 0px 5px 5px -3px var(--jp-shadow-umbra-color),
    0px 8px 10px 1px var(--jp-shadow-penumbra-color),
    0px 3px 14px 2px var(--jp-shadow-ambient-color);
  --jp-elevation-z12: 0px 7px 8px -4px var(--jp-shadow-umbra-color),
    0px 12px 17px 2px var(--jp-shadow-penumbra-color),
    0px 5px 22px 4px var(--jp-shadow-ambient-color);
  --jp-elevation-z16: 0px 8px 10px -5px var(--jp-shadow-umbra-color),
    0px 16px 24px 2px var(--jp-shadow-penumbra-color),
    0px 6px 30px 5px var(--jp-shadow-ambient-color);
  --jp-elevation-z20: 0px 10px 13px -6px var(--jp-shadow-umbra-color),
    0px 20px 31px 3px var(--jp-shadow-penumbra-color),
    0px 8px 38px 7px var(--jp-shadow-ambient-color);
  --jp-elevation-z24: 0px 11px 15px -7px var(--jp-shadow-umbra-color),
    0px 24px 38px 3px var(--jp-shadow-penumbra-color),
    0px 9px 46px 8px var(--jp-shadow-ambient-color);

  /* Borders
   *
   * The following variables, specify the visual styling of borders in JupyterLab.
   */

  --jp-border-width: 1px;
  --jp-border-color0: var(--md-grey-400);
  --jp-border-color1: var(--md-grey-400);
  --jp-border-color2: var(--md-grey-300);
  --jp-border-color3: var(--md-grey-200);
  --jp-border-radius: 2px;

  /* UI Fonts
   *
   * The UI font CSS variables are used for the typography all of the JupyterLab
   * user interface elements that are not directly user generated content.
   *
   * The font sizing here is done assuming that the body font size of --jp-ui-font-size1
   * is applied to a parent element. When children elements, such as headings, are sized
   * in em all things will be computed relative to that body size.
   */

  --jp-ui-font-scale-factor: 1.2;
  --jp-ui-font-size0: 0.83333em;
  --jp-ui-font-size1: 13px; /* Base font size */
  --jp-ui-font-size2: 1.2em;
  --jp-ui-font-size3: 1.44em;

  --jp-ui-font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica,
    Arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol';

  /*
   * Use these font colors against the corresponding main layout colors.
   * In a light theme, these go from dark to light.
   */

  /* Defaults use Material Design specification */
  --jp-ui-font-color0: rgba(0, 0, 0, 1);
  --jp-ui-font-color1: rgba(0, 0, 0, 0.87);
  --jp-ui-font-color2: rgba(0, 0, 0, 0.54);
  --jp-ui-font-color3: rgba(0, 0, 0, 0.38);

  /*
   * Use these against the brand/accent/warn/error colors.
   * These will typically go from light to darker, in both a dark and light theme.
   */

  --jp-ui-inverse-font-color0: rgba(255, 255, 255, 1);
  --jp-ui-inverse-font-color1: rgba(255, 255, 255, 1);
  --jp-ui-inverse-font-color2: rgba(255, 255, 255, 0.7);
  --jp-ui-inverse-font-color3: rgba(255, 255, 255, 0.5);

  /* Content Fonts
   *
   * Content font variables are used for typography of user generated content.
   *
   * The font sizing here is done assuming that the body font size of --jp-content-font-size1
   * is applied to a parent element. When children elements, such as headings, are sized
   * in em all things will be computed relative to that body size.
   */

  --jp-content-line-height: 1.6;
  --jp-content-font-scale-factor: 1.2;
  --jp-content-font-size0: 0.83333em;
  --jp-content-font-size1: 14px; /* Base font size */
  --jp-content-font-size2: 1.2em;
  --jp-content-font-size3: 1.44em;
  --jp-content-font-size4: 1.728em;
  --jp-content-font-size5: 2.0736em;

  /* This gives a magnification of about 125% in presentation mode over normal. */
  --jp-content-presentation-font-size1: 17px;

  --jp-content-heading-line-height: 1;
  --jp-content-heading-margin-top: 1.2em;
  --jp-content-heading-margin-bottom: 0.8em;
  --jp-content-heading-font-weight: 500;

  /* Defaults use Material Design specification */
  --jp-content-font-color0: rgba(0, 0, 0, 1);
  --jp-content-font-color1: rgba(0, 0, 0, 0.87);
  --jp-content-font-color2: rgba(0, 0, 0, 0.54);
  --jp-content-font-color3: rgba(0, 0, 0, 0.38);

  --jp-content-link-color: var(--md-blue-700);

  --jp-content-font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI',
    Helvetica, Arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji',
    'Segoe UI Symbol';

  /*
   * Code Fonts
   *
   * Code font variables are used for typography of code and other monospaces content.
   */

  --jp-code-font-size: 13px;
  --jp-code-line-height: 1.3077; /* 17px for 13px base */
  --jp-code-padding: 5px; /* 5px for 13px base, codemirror highlighting needs integer px value */
  --jp-code-font-family-default: Menlo, Consolas, 'DejaVu Sans Mono', monospace;
  --jp-code-font-family: var(--jp-code-font-family-default);

  /* This gives a magnification of about 125% in presentation mode over normal. */
  --jp-code-presentation-font-size: 16px;

  /* may need to tweak cursor width if you change font size */
  --jp-code-cursor-width0: 1.4px;
  --jp-code-cursor-width1: 2px;
  --jp-code-cursor-width2: 4px;

  /* Layout
   *
   * The following are the main layout colors use in JupyterLab. In a light
   * theme these would go from light to dark.
   */

  --jp-layout-color0: white;
  --jp-layout-color1: white;
  --jp-layout-color2: var(--md-grey-200);
  --jp-layout-color3: var(--md-grey-400);
  --jp-layout-color4: var(--md-grey-600);

  /* Inverse Layout
   *
   * The following are the inverse layout colors use in JupyterLab. In a light
   * theme these would go from dark to light.
   */

  --jp-inverse-layout-color0: #111111;
  --jp-inverse-layout-color1: var(--md-grey-900);
  --jp-inverse-layout-color2: var(--md-grey-800);
  --jp-inverse-layout-color3: var(--md-grey-700);
  --jp-inverse-layout-color4: var(--md-grey-600);

  /* Brand/accent */

  --jp-brand-color0: var(--md-blue-900);
  --jp-brand-color1: var(--md-blue-700);
  --jp-brand-color2: var(--md-blue-300);
  --jp-brand-color3: var(--md-blue-100);
  --jp-brand-color4: var(--md-blue-50);

  --jp-accent-color0: var(--md-green-900);
  --jp-accent-color1: var(--md-green-700);
  --jp-accent-color2: var(--md-green-300);
  --jp-accent-color3: var(--md-green-100);

  /* State colors (warn, error, success, info) */

  --jp-warn-color0: var(--md-orange-900);
  --jp-warn-color1: var(--md-orange-700);
  --jp-warn-color2: var(--md-orange-300);
  --jp-warn-color3: var(--md-orange-100);

  --jp-error-color0: var(--md-red-900);
  --jp-error-color1: var(--md-red-700);
  --jp-error-color2: var(--md-red-300);
  --jp-error-color3: var(--md-red-100);

  --jp-success-color0: var(--md-green-900);
  --jp-success-color1: var(--md-green-700);
  --jp-success-color2: var(--md-green-300);
  --jp-success-color3: var(--md-green-100);

  --jp-info-color0: var(--md-cyan-900);
  --jp-info-color1: var(--md-cyan-700);
  --jp-info-color2: var(--md-cyan-300);
  --jp-info-color3: var(--md-cyan-100);

  /* Cell specific styles */

  --jp-cell-padding: 5px;

  --jp-cell-collapser-width: 8px;
  --jp-cell-collapser-min-height: 20px;
  --jp-cell-collapser-not-active-hover-opacity: 0.6;

  --jp-cell-editor-background: var(--md-grey-100);
  --jp-cell-editor-border-color: var(--md-grey-300);
  --jp-cell-editor-box-shadow: inset 0 0 2px var(--md-blue-300);
  --jp-cell-editor-active-background: var(--jp-layout-color0);
  --jp-cell-editor-active-border-color: var(--jp-brand-color1);

  --jp-cell-prompt-width: 64px;
  --jp-cell-prompt-font-family: var(--jp-code-font-family-default);
  --jp-cell-prompt-letter-spacing: 0px;
  --jp-cell-prompt-opacity: 1;
  --jp-cell-prompt-not-active-opacity: 0.5;
  --jp-cell-prompt-not-active-font-color: var(--md-grey-700);
  /* A custom blend of MD grey and blue 600
   * See https://meyerweb.com/eric/tools/color-blend/#546E7A:1E88E5:5:hex */
  --jp-cell-inprompt-font-color: #307fc1;
  /* A custom blend of MD grey and orange 600
   * https://meyerweb.com/eric/tools/color-blend/#546E7A:F4511E:5:hex */
  --jp-cell-outprompt-font-color: #bf5b3d;

  /* Notebook specific styles */

  --jp-notebook-padding: 10px;
  --jp-notebook-select-background: var(--jp-layout-color1);
  --jp-notebook-multiselected-color: var(--md-blue-50);

  /* The scroll padding is calculated to fill enough space at the bottom of the
  notebook to show one single-line cell (with appropriate padding) at the top
  when the notebook is scrolled all the way to the bottom. We also subtract one
  pixel so that no scrollbar appears if we have just one single-line cell in the
  notebook. This padding is to enable a 'scroll past end' feature in a notebook.
  */
  --jp-notebook-scroll-padding: calc(
    100% - var(--jp-code-font-size) * var(--jp-code-line-height) -
      var(--jp-code-padding) - var(--jp-cell-padding) - 1px
  );

  /* Rendermime styles */

  --jp-rendermime-error-background: #fdd;
  --jp-rendermime-table-row-background: var(--md-grey-100);
  --jp-rendermime-table-row-hover-background: var(--md-light-blue-50);

  /* Dialog specific styles */

  --jp-dialog-background: rgba(0, 0, 0, 0.25);

  /* Console specific styles */

  --jp-console-padding: 10px;

  /* Toolbar specific styles */

  --jp-toolbar-border-color: var(--jp-border-color1);
  --jp-toolbar-micro-height: 8px;
  --jp-toolbar-background: var(--jp-layout-color1);
  --jp-toolbar-box-shadow: 0px 0px 2px 0px rgba(0, 0, 0, 0.24);
  --jp-toolbar-header-margin: 4px 4px 0px 4px;
  --jp-toolbar-active-background: var(--md-grey-300);

  /* Statusbar specific styles */

  --jp-statusbar-height: 24px;

  /* Input field styles */

  --jp-input-box-shadow: inset 0 0 2px var(--md-blue-300);
  --jp-input-active-background: var(--jp-layout-color1);
  --jp-input-hover-background: var(--jp-layout-color1);
  --jp-input-background: var(--md-grey-100);
  --jp-input-border-color: var(--jp-border-color1);
  --jp-input-active-border-color: var(--jp-brand-color1);
  --jp-input-active-box-shadow-color: rgba(19, 124, 189, 0.3);

  /* General editor styles */

  --jp-editor-selected-background: #d9d9d9;
  --jp-editor-selected-focused-background: #d7d4f0;
  --jp-editor-cursor-color: var(--jp-ui-font-color0);

  /* Code mirror specific styles */

  --jp-mirror-editor-keyword-color: #008000;
  --jp-mirror-editor-atom-color: #88f;
  --jp-mirror-editor-number-color: #080;
  --jp-mirror-editor-def-color: #00f;
  --jp-mirror-editor-variable-color: var(--md-grey-900);
  --jp-mirror-editor-variable-2-color: #05a;
  --jp-mirror-editor-variable-3-color: #085;
  --jp-mirror-editor-punctuation-color: #05a;
  --jp-mirror-editor-property-color: #05a;
  --jp-mirror-editor-operator-color: #aa22ff;
  --jp-mirror-editor-comment-color: #408080;
  --jp-mirror-editor-string-color: #ba2121;
  --jp-mirror-editor-string-2-color: #708;
  --jp-mirror-editor-meta-color: #aa22ff;
  --jp-mirror-editor-qualifier-color: #555;
  --jp-mirror-editor-builtin-color: #008000;
  --jp-mirror-editor-bracket-color: #997;
  --jp-mirror-editor-tag-color: #170;
  --jp-mirror-editor-attribute-color: #00c;
  --jp-mirror-editor-header-color: blue;
  --jp-mirror-editor-quote-color: #090;
  --jp-mirror-editor-link-color: #00c;
  --jp-mirror-editor-error-color: #f00;
  --jp-mirror-editor-hr-color: #999;

  /* Vega extension styles */

  --jp-vega-background: white;

  /* Sidebar-related styles */

  --jp-sidebar-min-width: 250px;

  /* Search-related styles */

  --jp-search-toggle-off-opacity: 0.5;
  --jp-search-toggle-hover-opacity: 0.8;
  --jp-search-toggle-on-opacity: 1;
  --jp-search-selected-match-background-color: rgb(245, 200, 0);
  --jp-search-selected-match-color: black;
  --jp-search-unselected-match-background-color: var(
    --jp-inverse-layout-color0
  );
  --jp-search-unselected-match-color: var(--jp-ui-inverse-font-color0);

  /* Icon colors that work well with light or dark backgrounds */
  --jp-icon-contrast-color0: var(--md-purple-600);
  --jp-icon-contrast-color1: var(--md-green-600);
  --jp-icon-contrast-color2: var(--md-pink-600);
  --jp-icon-contrast-color3: var(--md-blue-600);
}
</style>

<style type="text/css">
/* Force rendering true colors when outputing to pdf */
* {
  -webkit-print-color-adjust: exact;
}

/* Misc */
a.anchor-link {
  display: none;
}

.highlight  {
  margin: 0.4em;
}

/* Input area styling */
.jp-InputArea {
  overflow: hidden;
}

.jp-InputArea-editor {
  overflow: hidden;
}

.CodeMirror pre {
  margin: 0;
  padding: 0;
}

/* Using table instead of flexbox so that we can use break-inside property */
/* CSS rules under this comment should not be required anymore after we move to the JupyterLab 4.0 CSS */


.jp-CodeCell.jp-mod-outputsScrolled .jp-OutputArea-prompt {
  min-width: calc(
    var(--jp-cell-prompt-width) - var(--jp-private-cell-scrolling-output-offset)
  );
}

.jp-OutputArea-child {
  display: table;
  width: 100%;
}

.jp-OutputPrompt {
  display: table-cell;
  vertical-align: top;
  min-width: var(--jp-cell-prompt-width);
}

body[data-format='mobile'] .jp-OutputPrompt {
  display: table-row;
}

.jp-OutputArea-output {
  display: table-cell;
  width: 100%;
}

body[data-format='mobile'] .jp-OutputArea-child .jp-OutputArea-output {
  display: table-row;
}

.jp-OutputArea-output.jp-OutputArea-executeResult {
  width: 100%;
}

/* Hiding the collapser by default */
.jp-Collapser {
  display: none;
}

@media print {
  .jp-Cell-inputWrapper,
  .jp-Cell-outputWrapper {
    display: block;
  }

  .jp-OutputArea-child {
    break-inside: avoid-page;
  }
}
</style>

<!-- Load mathjax -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.7/latest.js?config=TeX-AMS_CHTML-full,Safe"> </script>
    <!-- MathJax configuration -->
    <script type="text/x-mathjax-config">
    init_mathjax = function() {
        if (window.MathJax) {
        // MathJax loaded
            MathJax.Hub.Config({
                TeX: {
                    equationNumbers: {
                    autoNumber: "AMS",
                    useLabelIds: true
                    }
                },
                tex2jax: {
                    inlineMath: [ ['$','$'], ["\\(","\\)"] ],
                    displayMath: [ ['$$','$$'], ["\\[","\\]"] ],
                    processEscapes: true,
                    processEnvironments: true
                },
                displayAlign: 'center',
                CommonHTML: {
                    linebreaks: { 
                    automatic: true 
                    }
                }
            });
        
            MathJax.Hub.Queue(["Typeset", MathJax.Hub]);
        }
    }
    init_mathjax();
    </script>
    <!-- End of mathjax configuration --></head>
<body class="jp-Notebook" data-jp-theme-light="true" data-jp-theme-name="JupyterLab Light">

<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">
<h1 id="Source">Source<a class="anchor-link" href="#Source">&#182;</a></h1><p><a href="https://programminghistorian.org/en/lessons/clustering-with-scikit-learn-in-python">https://programminghistorian.org/en/lessons/clustering-with-scikit-learn-in-python</a></p>

</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">
<h1 id="Reflection">Reflection<a class="anchor-link" href="#Reflection">&#182;</a></h1><p>Clustering is a complicated topic with many parts. The goal of clustering is to divide the data into several groups or clusters. Each group should be rather unique and ideally, each data point should belong to a definite group, with ideally no data lying in between. It is like sorting a collection of movies by genre. Some movies might be more full of action than others, but each movie belongs to a category and, if done correctly, only one category. The problem is, just like when sorting those movies, how do you know what categories you are going to have ahead of time? Well luckily clustering can do that mostly by looking at the arrangement of the data, but you still have to define how many clusters you want. Maybe you only have horror, action, and comedy movies so you want three clusters.</p>
<p>Clustering is a hard topic to understand. As a result, this article written by Thomas Jurczyk is a long article with high difficulty. To say the least, I might have gone a bit overboard choosing to write a report on this article, but still found a way to finish it all anyways (though my commenting fell off near the end). I even got some warnings that are hard to fix, but luckily do not break anything so it was not an issue. I choose this article as I might do something similar in my final project, but not to this extreme.</p>

</div>
</div>
</div>
</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">
<h1 id="Code">Code<a class="anchor-link" href="#Code">&#182;</a></h1>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs  ">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&nbsp;[1]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
     <div class="CodeMirror cm-s-jupyter">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># First import all nessecary libraries</span>
<span class="kn">import</span> <span class="nn">pandas</span> <span class="k">as</span> <span class="nn">pd</span>
<span class="kn">import</span> <span class="nn">numpy</span> <span class="k">as</span> <span class="nn">np</span>
<span class="kn">from</span> <span class="nn">sklearn.preprocessing</span> <span class="kn">import</span> <span class="n">StandardScaler</span> <span class="k">as</span> <span class="n">SS</span> <span class="c1"># z-score standardization </span>
<span class="kn">from</span> <span class="nn">sklearn.cluster</span> <span class="kn">import</span> <span class="n">KMeans</span><span class="p">,</span> <span class="n">DBSCAN</span> <span class="c1"># clustering algorithms</span>
<span class="kn">from</span> <span class="nn">sklearn.decomposition</span> <span class="kn">import</span> <span class="n">PCA</span> <span class="c1"># dimensionality reduction</span>
<span class="kn">from</span> <span class="nn">sklearn.metrics</span> <span class="kn">import</span> <span class="n">silhouette_score</span> <span class="c1"># used as a metric to evaluate the cohesion in a cluster</span>
<span class="kn">from</span> <span class="nn">sklearn.neighbors</span> <span class="kn">import</span> <span class="n">NearestNeighbors</span> <span class="c1"># for selecting the optimal eps value when using DBSCAN</span>
<span class="kn">from</span> <span class="nn">sklearn.feature_extraction.text</span> <span class="kn">import</span> <span class="n">TfidfVectorizer</span>

<span class="c1"># plotting libraries</span>
<span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="k">as</span> <span class="nn">plt</span>
<span class="kn">import</span> <span class="nn">seaborn</span> <span class="k">as</span> <span class="nn">sns</span>
<span class="kn">from</span> <span class="nn">yellowbrick.cluster</span> <span class="kn">import</span> <span class="n">SilhouetteVisualizer</span>

<span class="n">pd</span><span class="o">.</span><span class="n">set_option</span><span class="p">(</span><span class="s1">&#39;display.max_colwidth&#39;</span><span class="p">,</span> <span class="kc">None</span><span class="p">)</span>
<span class="n">df_authors</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="s2">&quot;DNP_ancient_authors.csv&quot;</span><span class="p">,</span> <span class="n">index_col</span><span class="o">=</span><span class="s2">&quot;authors&quot;</span><span class="p">)</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="n">columns</span><span class="o">=</span><span class="p">[</span><span class="s2">&quot;Unnamed: 0&quot;</span><span class="p">])</span>
</pre></div>

     </div>
</div>
</div>
</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell   ">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&nbsp;[2]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
     <div class="CodeMirror cm-s-jupyter">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">ninety_quantile</span> <span class="o">=</span> <span class="n">df_authors</span><span class="p">[</span><span class="s2">&quot;word_count&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">quantile</span><span class="p">(</span><span class="mf">0.9</span><span class="p">)</span>
<span class="n">df_authors</span> <span class="o">=</span> <span class="n">df_authors</span><span class="p">[</span><span class="n">df_authors</span><span class="p">[</span><span class="s2">&quot;word_count&quot;</span><span class="p">]</span> <span class="o">&lt;=</span> <span class="n">ninety_quantile</span><span class="p">]</span>

<span class="n">df_authors</span><span class="o">.</span><span class="n">describe</span><span class="p">()</span>
</pre></div>

     </div>
</div>
</div>
</div>

<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>


<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt">Out[2]:</div>



<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/html">
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>word_count</th>
      <th>modern_translations</th>
      <th>known_works</th>
      <th>manuscripts</th>
      <th>early_editions</th>
      <th>early_translations</th>
      <th>modern_editions</th>
      <th>commentaries</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>214.000000</td>
      <td>214.000000</td>
      <td>214.000000</td>
      <td>214.000000</td>
      <td>214.000000</td>
      <td>214.000000</td>
      <td>214.000000</td>
      <td>214.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>725.420561</td>
      <td>10.247664</td>
      <td>3.588785</td>
      <td>3.864486</td>
      <td>5.219626</td>
      <td>3.803738</td>
      <td>8.462617</td>
      <td>2.915888</td>
    </tr>
    <tr>
      <th>std</th>
      <td>391.536699</td>
      <td>9.036669</td>
      <td>4.153065</td>
      <td>3.934362</td>
      <td>3.437352</td>
      <td>4.896946</td>
      <td>6.905533</td>
      <td>5.421435</td>
    </tr>
    <tr>
      <th>min</th>
      <td>99.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>427.500000</td>
      <td>4.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>3.000000</td>
      <td>0.000000</td>
      <td>4.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>651.000000</td>
      <td>8.000000</td>
      <td>2.000000</td>
      <td>3.000000</td>
      <td>5.000000</td>
      <td>2.000000</td>
      <td>6.000000</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>951.000000</td>
      <td>14.000000</td>
      <td>5.000000</td>
      <td>6.000000</td>
      <td>7.000000</td>
      <td>6.000000</td>
      <td>12.000000</td>
      <td>3.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>1772.000000</td>
      <td>67.000000</td>
      <td>24.000000</td>
      <td>34.000000</td>
      <td>17.000000</td>
      <td>30.000000</td>
      <td>35.000000</td>
      <td>42.000000</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>

</div>

</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">
<h3 id="Ancient-Authors-Dataset">Ancient Authors Dataset<a class="anchor-link" href="#Ancient-Authors-Dataset">&#182;</a></h3>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs  ">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&nbsp;[3]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
     <div class="CodeMirror cm-s-jupyter">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Functions</span>

<span class="k">def</span> <span class="nf">silhouettePlot</span><span class="p">(</span><span class="n">range_</span><span class="p">,</span> <span class="n">data</span><span class="p">):</span>
    <span class="sd">&#39;&#39;&#39;</span>
<span class="sd">    we will use this function to plot a silhouette plot that helps us to evaluate the cohesion in clusters (k-means only)</span>
<span class="sd">    &#39;&#39;&#39;</span>
    <span class="n">half_length</span> <span class="o">=</span> <span class="nb">int</span><span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">range_</span><span class="p">)</span><span class="o">/</span><span class="mi">2</span><span class="p">)</span>
    <span class="n">range_list</span> <span class="o">=</span> <span class="nb">list</span><span class="p">(</span><span class="n">range_</span><span class="p">)</span>
    <span class="n">fig</span><span class="p">,</span> <span class="n">ax</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">subplots</span><span class="p">(</span><span class="n">half_length</span><span class="p">,</span> <span class="mi">2</span><span class="p">,</span> <span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">15</span><span class="p">,</span><span class="mi">8</span><span class="p">))</span>
    <span class="k">for</span> <span class="n">_</span> <span class="ow">in</span> <span class="n">range_</span><span class="p">:</span>
        <span class="n">kmeans</span> <span class="o">=</span> <span class="n">KMeans</span><span class="p">(</span><span class="n">n_clusters</span><span class="o">=</span><span class="n">_</span><span class="p">,</span> <span class="n">random_state</span><span class="o">=</span><span class="mi">42</span><span class="p">)</span>
        <span class="n">q</span><span class="p">,</span> <span class="n">mod</span> <span class="o">=</span> <span class="nb">divmod</span><span class="p">(</span><span class="n">_</span> <span class="o">-</span> <span class="n">range_list</span><span class="p">[</span><span class="mi">0</span><span class="p">],</span> <span class="mi">2</span><span class="p">)</span>
        <span class="n">sv</span> <span class="o">=</span> <span class="n">SilhouetteVisualizer</span><span class="p">(</span><span class="n">kmeans</span><span class="p">,</span> <span class="n">colors</span><span class="o">=</span><span class="s2">&quot;yellowbrick&quot;</span><span class="p">,</span> <span class="n">ax</span><span class="o">=</span><span class="n">ax</span><span class="p">[</span><span class="n">q</span><span class="p">][</span><span class="n">mod</span><span class="p">])</span>
        <span class="n">ax</span><span class="p">[</span><span class="n">q</span><span class="p">][</span><span class="n">mod</span><span class="p">]</span><span class="o">.</span><span class="n">set_title</span><span class="p">(</span><span class="s2">&quot;Silhouette Plot with n=</span><span class="si">{}</span><span class="s2"> Cluster&quot;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">_</span><span class="p">))</span>
        <span class="n">sv</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">data</span><span class="p">)</span>
    <span class="n">fig</span><span class="o">.</span><span class="n">tight_layout</span><span class="p">()</span>
    <span class="n">fig</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
    <span class="n">fig</span><span class="o">.</span><span class="n">savefig</span><span class="p">(</span><span class="s2">&quot;silhouette_plot.png&quot;</span><span class="p">)</span>

    
<span class="k">def</span> <span class="nf">elbowPlot</span><span class="p">(</span><span class="n">range_</span><span class="p">,</span> <span class="n">data</span><span class="p">,</span> <span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">10</span><span class="p">,</span><span class="mi">10</span><span class="p">)):</span>
    <span class="sd">&#39;&#39;&#39;</span>
<span class="sd">    the elbow plot function helps to figure out the right amount of clusters for a dataset</span>
<span class="sd">    &#39;&#39;&#39;</span>
    <span class="n">inertia_list</span> <span class="o">=</span> <span class="p">[]</span>
    <span class="k">for</span> <span class="n">n</span> <span class="ow">in</span> <span class="n">range_</span><span class="p">:</span>
        <span class="n">kmeans</span> <span class="o">=</span> <span class="n">KMeans</span><span class="p">(</span><span class="n">n_clusters</span><span class="o">=</span><span class="n">n</span><span class="p">,</span> <span class="n">random_state</span><span class="o">=</span><span class="mi">42</span><span class="p">)</span>
        <span class="n">kmeans</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">data</span><span class="p">)</span>
        <span class="n">inertia_list</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">kmeans</span><span class="o">.</span><span class="n">inertia_</span><span class="p">)</span>
        
    <span class="c1"># plotting</span>
    <span class="n">fig</span> <span class="o">=</span> <span class="n">plt</span><span class="o">.</span><span class="n">figure</span><span class="p">(</span><span class="n">figsize</span><span class="o">=</span><span class="n">figsize</span><span class="p">)</span>
    <span class="n">ax</span> <span class="o">=</span> <span class="n">fig</span><span class="o">.</span><span class="n">add_subplot</span><span class="p">(</span><span class="mi">111</span><span class="p">)</span>
    <span class="n">sns</span><span class="o">.</span><span class="n">lineplot</span><span class="p">(</span><span class="n">y</span><span class="o">=</span><span class="n">inertia_list</span><span class="p">,</span> <span class="n">x</span><span class="o">=</span><span class="n">range_</span><span class="p">,</span> <span class="n">ax</span><span class="o">=</span><span class="n">ax</span><span class="p">)</span>
    <span class="n">ax</span><span class="o">.</span><span class="n">set_xlabel</span><span class="p">(</span><span class="s2">&quot;Cluster&quot;</span><span class="p">)</span>
    <span class="n">ax</span><span class="o">.</span><span class="n">set_ylabel</span><span class="p">(</span><span class="s2">&quot;Inertia&quot;</span><span class="p">)</span>
    <span class="n">ax</span><span class="o">.</span><span class="n">set_xticks</span><span class="p">(</span><span class="nb">list</span><span class="p">(</span><span class="n">range_</span><span class="p">))</span>
    <span class="n">fig</span><span class="o">.</span><span class="n">show</span><span class="p">()</span>
    <span class="n">fig</span><span class="o">.</span><span class="n">savefig</span><span class="p">(</span><span class="s2">&quot;elbow_plot.png&quot;</span><span class="p">)</span>
    

<span class="k">def</span> <span class="nf">findOptimalEps</span><span class="p">(</span><span class="n">n_neighbors</span><span class="p">,</span> <span class="n">data</span><span class="p">):</span>
    <span class="sd">&#39;&#39;&#39;</span>
<span class="sd">    function to find optimal eps distance when using DBSCAN; based on this article: https://towardsdatascience.com/machine-learning-clustering-dbscan-determine-the-optimal-value-for-epsilon-eps-python-example-3100091cfbc</span>
<span class="sd">    &#39;&#39;&#39;</span>
    <span class="n">neigh</span> <span class="o">=</span> <span class="n">NearestNeighbors</span><span class="p">(</span><span class="n">n_neighbors</span><span class="o">=</span><span class="n">n_neighbors</span><span class="p">)</span>
    <span class="n">nbrs</span> <span class="o">=</span> <span class="n">neigh</span><span class="o">.</span><span class="n">fit</span><span class="p">(</span><span class="n">data</span><span class="p">)</span>
    <span class="n">distances</span><span class="p">,</span> <span class="n">indices</span> <span class="o">=</span> <span class="n">nbrs</span><span class="o">.</span><span class="n">kneighbors</span><span class="p">(</span><span class="n">data</span><span class="p">)</span>
    <span class="n">distances</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">sort</span><span class="p">(</span><span class="n">distances</span><span class="p">,</span> <span class="n">axis</span><span class="o">=</span><span class="mi">0</span><span class="p">)</span>
    <span class="n">distances</span> <span class="o">=</span> <span class="n">distances</span><span class="p">[:,</span><span class="mi">1</span><span class="p">]</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">plot</span><span class="p">(</span><span class="n">distances</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s2">&quot;Data Points&quot;</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s2">&quot;Distance&quot;</span><span class="p">)</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">savefig</span><span class="p">(</span><span class="s2">&quot;eps_plot.png&quot;</span><span class="p">)</span>


<span class="k">def</span> <span class="nf">progressiveFeatureSelection</span><span class="p">(</span><span class="n">df</span><span class="p">,</span> <span class="n">n_clusters</span><span class="o">=</span><span class="mi">3</span><span class="p">,</span> <span class="n">max_features</span><span class="o">=</span><span class="mi">4</span><span class="p">,):</span>
    <span class="sd">&#39;&#39;&#39;</span>
<span class="sd">    very basic implementation of an algorithm for feature selection (unsupervised clustering); taken from this post: https://datascience.stackexchange.com/questions/67040/how-to-do-feature-selection-for-clustering-and-implement-it-in-python</span>
<span class="sd">    &#39;&#39;&#39;</span>
    <span class="n">feature_list</span> <span class="o">=</span> <span class="nb">list</span><span class="p">(</span><span class="n">df</span><span class="o">.</span><span class="n">columns</span><span class="p">)</span>
    <span class="n">selected_features</span> <span class="o">=</span> <span class="nb">list</span><span class="p">()</span>
    <span class="c1"># select starting feature</span>
    <span class="n">initial_feature</span> <span class="o">=</span> <span class="s2">&quot;&quot;</span>
    <span class="n">high_score</span> <span class="o">=</span> <span class="mi">0</span>
    <span class="k">for</span> <span class="n">feature</span> <span class="ow">in</span> <span class="n">feature_list</span><span class="p">:</span>
        <span class="n">kmeans</span> <span class="o">=</span> <span class="n">KMeans</span><span class="p">(</span><span class="n">n_clusters</span><span class="o">=</span><span class="n">n_clusters</span><span class="p">,</span> <span class="n">random_state</span><span class="o">=</span><span class="mi">42</span><span class="p">)</span>
        <span class="n">data_</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">feature</span><span class="p">]</span>
        <span class="n">labels</span> <span class="o">=</span> <span class="n">kmeans</span><span class="o">.</span><span class="n">fit_predict</span><span class="p">(</span><span class="n">data_</span><span class="o">.</span><span class="n">to_frame</span><span class="p">())</span>
        <span class="n">score_</span> <span class="o">=</span> <span class="n">silhouette_score</span><span class="p">(</span><span class="n">data_</span><span class="o">.</span><span class="n">to_frame</span><span class="p">(),</span> <span class="n">labels</span><span class="p">)</span>
        <span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Proposed new feature </span><span class="si">{}</span><span class="s2"> with score </span><span class="si">{}</span><span class="s2">&quot;</span><span class="o">.</span> <span class="nb">format</span><span class="p">(</span><span class="n">feature</span><span class="p">,</span> <span class="n">score_</span><span class="p">))</span>
        <span class="k">if</span> <span class="n">score_</span> <span class="o">&gt;=</span> <span class="n">high_score</span><span class="p">:</span>
            <span class="n">initial_feature</span> <span class="o">=</span> <span class="n">feature</span>
            <span class="n">high_score</span> <span class="o">=</span> <span class="n">score_</span>
    <span class="nb">print</span><span class="p">(</span><span class="s2">&quot;The initial feature is </span><span class="si">{}</span><span class="s2"> with a silhouette score of </span><span class="si">{}</span><span class="s2">.&quot;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">initial_feature</span><span class="p">,</span> <span class="n">high_score</span><span class="p">))</span>
    <span class="n">feature_list</span><span class="o">.</span><span class="n">remove</span><span class="p">(</span><span class="n">initial_feature</span><span class="p">)</span>
    <span class="n">selected_features</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">initial_feature</span><span class="p">)</span>
    <span class="k">for</span> <span class="n">_</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">max_features</span><span class="o">-</span><span class="mi">1</span><span class="p">):</span>
        <span class="n">high_score</span> <span class="o">=</span> <span class="mi">0</span>
        <span class="n">selected_feature</span> <span class="o">=</span> <span class="s2">&quot;&quot;</span>
        <span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Starting selection </span><span class="si">{}</span><span class="s2">...&quot;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">_</span><span class="p">))</span>
        <span class="k">for</span> <span class="n">feature</span> <span class="ow">in</span> <span class="n">feature_list</span><span class="p">:</span>
            <span class="n">selection_</span> <span class="o">=</span> <span class="n">selected_features</span><span class="o">.</span><span class="n">copy</span><span class="p">()</span>
            <span class="n">selection_</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">feature</span><span class="p">)</span>
            <span class="n">kmeans</span> <span class="o">=</span> <span class="n">KMeans</span><span class="p">(</span><span class="n">n_clusters</span><span class="o">=</span><span class="n">n_clusters</span><span class="p">,</span> <span class="n">random_state</span><span class="o">=</span><span class="mi">42</span><span class="p">)</span>
            <span class="n">data_</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="n">selection_</span><span class="p">]</span>
            <span class="n">labels</span> <span class="o">=</span> <span class="n">kmeans</span><span class="o">.</span><span class="n">fit_predict</span><span class="p">(</span><span class="n">data_</span><span class="p">)</span>
            <span class="n">score_</span> <span class="o">=</span> <span class="n">silhouette_score</span><span class="p">(</span><span class="n">data_</span><span class="p">,</span> <span class="n">labels</span><span class="p">)</span>
            <span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Proposed new feature </span><span class="si">{}</span><span class="s2"> with score </span><span class="si">{}</span><span class="s2">&quot;</span><span class="o">.</span> <span class="nb">format</span><span class="p">(</span><span class="n">feature</span><span class="p">,</span> <span class="n">score_</span><span class="p">))</span>
            <span class="k">if</span> <span class="n">score_</span> <span class="o">&gt;</span> <span class="n">high_score</span><span class="p">:</span>
                <span class="n">selected_feature</span> <span class="o">=</span> <span class="n">feature</span>
                <span class="n">high_score</span> <span class="o">=</span> <span class="n">score_</span>
        <span class="n">selected_features</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">selected_feature</span><span class="p">)</span>
        <span class="n">feature_list</span><span class="o">.</span><span class="n">remove</span><span class="p">(</span><span class="n">selected_feature</span><span class="p">)</span>
        <span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Selected new feature </span><span class="si">{}</span><span class="s2"> with score </span><span class="si">{}</span><span class="s2">&quot;</span><span class="o">.</span> <span class="nb">format</span><span class="p">(</span><span class="n">selected_feature</span><span class="p">,</span> <span class="n">high_score</span><span class="p">))</span>
    <span class="k">return</span> <span class="n">selected_features</span>
</pre></div>

     </div>
</div>
</div>
</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs  ">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&nbsp;[4]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
     <div class="CodeMirror cm-s-jupyter">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Next initialize scikit-learn&#39;s StandardScaler() to standardize our data</span>
<span class="n">scaler</span> <span class="o">=</span> <span class="n">SS</span><span class="p">()</span>

<span class="n">DNP_authors_standardized</span> <span class="o">=</span> <span class="n">scaler</span><span class="o">.</span><span class="n">fit_transform</span><span class="p">(</span><span class="n">df_authors</span><span class="p">)</span>

<span class="n">df_authors_standardized</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">DataFrame</span><span class="p">(</span><span class="n">DNP_authors_standardized</span><span class="p">,</span> <span class="n">columns</span><span class="o">=</span><span class="p">[</span><span class="s2">&quot;word_count_standardized&quot;</span><span class="p">,</span> <span class="s2">&quot;modern_translations_standardized&quot;</span><span class="p">,</span> <span class="s2">&quot;known_works_standardized&quot;</span><span class="p">,</span> <span class="s2">&quot;manuscripts_standardized&quot;</span><span class="p">,</span> <span class="s2">&quot;early_editions_standardized&quot;</span><span class="p">,</span> <span class="s2">&quot;early_translations_standardized&quot;</span><span class="p">,</span> <span class="s2">&quot;modern_editions_standardized&quot;</span><span class="p">,</span> <span class="s2">&quot;commentaries_standardized&quot;</span><span class="p">])</span>
<span class="n">df_authors_standardized</span> <span class="o">=</span> <span class="n">df_authors_standardized</span><span class="o">.</span><span class="n">set_index</span><span class="p">(</span><span class="n">df_authors</span><span class="o">.</span><span class="n">index</span><span class="p">)</span>
</pre></div>

     </div>
</div>
</div>
</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell   ">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&nbsp;[5]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
     <div class="CodeMirror cm-s-jupyter">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Next look for features for our data. The article says to find the best 3 out of the 10 in the dataset.</span>
<span class="n">selected_features</span> <span class="o">=</span> <span class="n">progressiveFeatureSelection</span><span class="p">(</span><span class="n">df_authors_standardized</span><span class="p">,</span> <span class="n">max_features</span><span class="o">=</span><span class="mi">3</span><span class="p">,</span> <span class="n">n_clusters</span><span class="o">=</span><span class="mi">3</span><span class="p">)</span>
<span class="n">df_standardized_sliced</span> <span class="o">=</span> <span class="n">df_authors_standardized</span><span class="p">[</span><span class="n">selected_features</span><span class="p">]</span>

<span class="n">df_standardized_sliced</span>
</pre></div>

     </div>
</div>
</div>
</div>

<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>


<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt"></div>


<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="text/plain">
<pre>Proposed new feature word_count_standardized with score 0.5815823896749474
Proposed new feature modern_translations_standardized with score 0.592449382653205
Proposed new feature known_works_standardized with score 0.7606223362466435
Proposed new feature manuscripts_standardized with score 0.6193716240205519
Proposed new feature early_editions_standardized with score 0.6054575587243932
Proposed new feature early_translations_standardized with score 0.7025924996773049
Proposed new feature modern_editions_standardized with score 0.6267499859538754
Proposed new feature commentaries_standardized with score 0.7635590362947628
The initial feature is commentaries_standardized with a silhouette score of 0.7635590362947628.
Starting selection 0...
Proposed new feature word_count_standardized with score 0.49823573315720454
Proposed new feature modern_translations_standardized with score 0.48709861763555096
Proposed new feature known_works_standardized with score 0.6248907484676766
Proposed new feature manuscripts_standardized with score 0.4990467101238413
Proposed new feature early_editions_standardized with score 0.486228428741611
Proposed new feature early_translations_standardized with score 0.5733248510427374
Proposed new feature modern_editions_standardized with score 0.5746359517651854
Selected new feature known_works_standardized with score 0.6248907484676766
Starting selection 1...
Proposed new feature word_count_standardized with score 0.5146900270599629
Proposed new feature modern_translations_standardized with score 0.5115607116954545
Proposed new feature manuscripts_standardized with score 0.48236942054347287
Proposed new feature early_editions_standardized with score 0.4292187272499715
Proposed new feature early_translations_standardized with score 0.4860441014648876
Proposed new feature modern_editions_standardized with score 0.5434584440130673
Selected new feature modern_editions_standardized with score 0.5434584440130673
</pre>
</div>
</div>

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt">Out[5]:</div>



<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/html">
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>commentaries_standardized</th>
      <th>known_works_standardized</th>
      <th>modern_editions_standardized</th>
    </tr>
    <tr>
      <th>authors</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Achilles Tatius of Alexandria</th>
      <td>-0.354220</td>
      <td>-0.624805</td>
      <td>-0.938055</td>
    </tr>
    <tr>
      <th>Aelianus Tacticus</th>
      <td>-0.539105</td>
      <td>-0.624805</td>
      <td>-1.083206</td>
    </tr>
    <tr>
      <th>Aelianus, Claudius (Aelian)</th>
      <td>-0.539105</td>
      <td>-0.142104</td>
      <td>-0.212300</td>
    </tr>
    <tr>
      <th>Aeneas Tacticus</th>
      <td>-0.539105</td>
      <td>-0.624805</td>
      <td>-0.357451</td>
    </tr>
    <tr>
      <th>Aeschylus of Athens</th>
      <td>3.158605</td>
      <td>0.823299</td>
      <td>0.948907</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>Venantius Fortunatus, Honorius Clementianus</th>
      <td>-0.539105</td>
      <td>0.099247</td>
      <td>-0.792904</td>
    </tr>
    <tr>
      <th>Vergiliana Appendix</th>
      <td>1.124864</td>
      <td>1.306000</td>
      <td>0.803756</td>
    </tr>
    <tr>
      <th>Xenophon of Athens</th>
      <td>0.015551</td>
      <td>0.340598</td>
      <td>0.803756</td>
    </tr>
    <tr>
      <th>Xenophon of Ephesus</th>
      <td>-0.539105</td>
      <td>-0.624805</td>
      <td>-0.502602</td>
    </tr>
    <tr>
      <th>Zosimus</th>
      <td>-0.354220</td>
      <td>-0.624805</td>
      <td>-0.938055</td>
    </tr>
  </tbody>
</table>
<p>214 rows × 3 columns</p>
</div>
</div>

</div>

</div>

</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell   ">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&nbsp;[6]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
     <div class="CodeMirror cm-s-jupyter">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Now we have to figure out the right amount of clusters, a hard task but we will likely use 3 due to having 3 features</span>
<span class="n">elbowPlot</span><span class="p">(</span><span class="nb">range</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span><span class="mi">11</span><span class="p">),</span> <span class="n">df_standardized_sliced</span><span class="p">)</span>
</pre></div>

     </div>
</div>
</div>
</div>

<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>


<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt"></div>


<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="application/vnd.jupyter.stderr">
<pre>C:\Users\alexk\anaconda3\lib\site-packages\sklearn\cluster\_kmeans.py:1036: UserWarning: KMeans is known to have a memory leak on Windows with MKL, when there are less chunks than available threads. You can avoid it by setting the environment variable OMP_NUM_THREADS=1.
  warnings.warn(
C:\Users\alexk\AppData\Local\Temp\ipykernel_2952\2335342308.py:38: UserWarning: Matplotlib is currently using module://matplotlib_inline.backend_inline, which is a non-GUI backend, so cannot show the figure.
  fig.show()
</pre>
</div>
</div>

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt"></div>




<div class="jp-RenderedImage jp-OutputArea-output ">
<img src="data:image/png;base64,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
"
class="
"
>
</div>

</div>

</div>

</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell   ">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&nbsp;[7]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
     <div class="CodeMirror cm-s-jupyter">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">silhouettePlot</span><span class="p">(</span><span class="nb">range</span><span class="p">(</span><span class="mi">3</span><span class="p">,</span><span class="mi">9</span><span class="p">),</span> <span class="n">df_standardized_sliced</span><span class="p">)</span>
</pre></div>

     </div>
</div>
</div>
</div>

<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>


<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt"></div>


<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="application/vnd.jupyter.stderr">
<pre>C:\Users\alexk\AppData\Local\Temp\ipykernel_2952\2335342308.py:17: UserWarning: Matplotlib is currently using module://matplotlib_inline.backend_inline, which is a non-GUI backend, so cannot show the figure.
  fig.show()
</pre>
</div>
</div>

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt"></div>




<div class="jp-RenderedImage jp-OutputArea-output ">
<img src="data:image/png;base64,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+Oijjw7ZuDjzzDP9uAYMGIA9e/bgnXfeOWTXzOuvvx6nnnoqAOCss87CWWedhXXr1uGyyy7DU089BSmznc2klHAcp9042zN58mR873vfw8KFC3HyySfji1/8Iqqrq5tts3//frz44ovYs2cP7r33Xn/dli1bUFtbC8Mw2jznRESU39imyMZRSG2Kt99+G4Zh4MILL8S777572M9nm4Ko+5iwIMpRX1+Pl156CZdffjmmTZuGadOm4brrrsOsWbPw/PPPo7y8/LDvNQz3PychBABAaw3HcfzngPsHP5VK+c+11v7jpqYmAG5xpng83iyr/+GHH/pdCQ/HcRxcfvnlqKurA+COnd2zZ88ht2053vRQ0ul0s9gz8ebGfygzZszA5z//eYwaNQpTp05FSUkJ/vznP+PVV1/FN77xjTbfC2SPI+Aey9xjlMu27VbbtXU35K233sKuXbv8Owvz5s3D8uXLsWfPnmbntba2Fv/617/Q0NDQ7I7Izp07ccstt7Q53ji30Thy5Eg89dRT2LBhA1544QVceumluO222zB9+nR/G8dxoLXG2rVr/Ybdxx9/DNu2sXv3bliW1ex4EBFR/8E2RVahtSkuvPBCHDx4EHPmzEFTU5P/+D//8z8xePBgfzu2KYi6jzUsiHJUVFTg/vvvx9/+9jd/3a5du9DQ0IDx48d3en+nnnoqHn30UX/85Zo1a/CpT30KlmWhoqICGzduBAC8/vrreO211wAAo0ePRigU8v9I7tixA7NmzfK3VUr5f+BzH59yyil45JFH0NDQAAC49957ceONN3blMAAAxowZA8Mw8Pvf/x6A+8f1d7/7HU4++eRWn51ryJAhKC8vx9q1azF16lSccsop+P3vf49PPvkEEyZMaLX94fbT03bt2oXrrrvOHxv6q1/9CuPGjWvVYBw8eDBmz56NJUuW+MeyoaEBt956K8rKyhAKhZptX1FR4Vch//Wvf+2v/9nPfoabb74Zp5xyCm644Qaccsop2Lx5M4Dsd47FYjjuuOPw0EMPAQD27t3b6UJlRESUn9imyCq0NsUjjzyCX//613jiiSfwn//5n/4xzk1WAGxTEPUEptmIcowePRr33Xcfvve97+H999+HbduIx+O44447MGbMGL+4VUddeOGF2LFjB+bPnw/HcVBdXY277roLALB48WLcdNNN+NOf/oQxY8b4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gqiPOVojldZIawcCAlLAHWrh9YKwvcREachCadhERcRGVVkU5RELSrJ6MxEREfVPWmsk0w601rCVQshyp9q0DXfoQ8jIfewubcO9OROzTURMhZCZHRrBmzNEhY8JCypqmax9k+MWjbRNt7tfZpyhFG5CIfM4U8dBCgEl4L7ujV2U3rjFzHZSCih466XA66lPUDNuKMKmO/awJGQiYhnu2ET+0aWg3Hefu7zqqmDjICKiwDheD4bMzRSVqcug3JoLUkhv6a5TmW1kts2UqeOQqccghUD8wMcYP3IADG8oRcwyMbjELRQZtQy2ffIF2wKUx5iwKBKjS20MGF4edBh5xZQKMdvAgKiFofEwSkIWjF6cf7p83w5MHjOo1/ZP1CUrV7pLNlKIqECNK7cxhG2gZgTcIRTuMFKFsClRGrYQt0yELbenQ0/0YKhv+hCTjx7RQ1FTr2FbgPIYExZF4tjKKCbXVAUdBhEREVGfOmFwjG0gIqJ+qkcTFo7j4NZbb8Vrr70Gy7Jw++23o7q6uic/goiIiIoA2xRERETUo/3fn376aSSTSfziF7/A//pf/wvf/va3e3L3REREVCTYpiAiIqIeTVjU19fjVG8e3+OOOw4bN27syd0TERFRkWCbgoiIiHp0SEhDQwNisZj/XCmFVCoFw2j9MVprAEAymezJEKgNiUQi6BCKHs9B8HgOWqisdJd9fFx4HoLXnXOQ+dud+VveGzrTpsiNJZ8TG/X19UGHULR47IPDYx+cjh778WVlAICtPFc9ir/7nXO4NkWPJixisRgaGxv9547jHLZh0dTUBADYunVrT4ZAbcjnRlyx4DkIHs9BCw884C77+LjwPASvJ85BU1MTQqFQD0TTWmfaFJlYiIio87b+8IdBh0B02DZFjyYsjj/+ePzhD3/Aueeei3/84x8YP378YbeNRqMYP348TNPkHMxERET9iNYaTU1NiEajvfYZnWlTAGxXEBER9UfttSmE7sH+nJmK3lu3boXWGnfccQeOOOKInto9ERERFQm2KYiIiKhHExZERERERERERD2hR2cJISIiIiIiIiLqCUxYEBEREREREVHeYcKCiIiIiIiIiPIOExZERERERERElHd6dFpTClamovprr70Gy7Jw++23o7q62n/9mWeewX333QfDMDBv3jwsWLAgwGgLV3vn4de//jV+/OMfQymF8ePH49Zbb4WUzB32pPbOQcYtt9yC0tJSXH/99QFEWdjaOwevvPIKvv3tb0NrjcrKSqxcuRK2bQcYceFp7xw8+eSTeOihhyClxLx581BXVxdgtIXl4MGDuOGGG/DRRx8hGo3izjvvREVFRbNt/uu//gv/7//9PwDA6aefjn//938PItSCwTZQcNjuCRbbPMFhW6ePaCoYv/vd7/TXvvY1rbXWL730kr7yyiv915LJpD7rrLP0J598ohOJhJ47d67+4IMPggq1oLV1Hg4cOKDPPPNMvX//fq211tdee61++umnA4mzkLV1DjJ+/vOf6wULFuiVK1f2dXhFoa1z4DiOPu+88/Sbb76ptdZ63bp1etu2bYHEWcja++9g6tSpevfu3TqRSPh/H6hn/OhHP9Lf//73tdZa//rXv9YrVqxo9vrbb7+tL7jgAp1KpXQ6ndYXXXSR/p//+Z8gQi0YbAMFh+2eYLHNExy2dfoG05sFpL6+HqeeeioA4LjjjsPGjRv917Zt24aqqiqUlpbCsixMnjwZf/vb34IKtaC1dR4sy8LatWsRDocBAKlUipnWXtDWOQCAl156CS+//DIuuuiiIMIrCm2dgzfeeANlZWX48Y9/jC984Qv45JNPMGbMmKBCLVjt/Xdw5JFHYt++fUgmk9BaQwgRRJgFKffYn3baafjrX//a7PUhQ4bgBz/4AZRSkFLyb0EPYBsoOGz3BIttnuCwrdM3mLAoIA0NDYjFYv5zpRRSqZT/Wjwe91+LRqNoaGjo8xiLQVvnQUqJgQMHAgDWrFmD/fv3Y+rUqYHEWcjaOgcffPAB/vf//t9YtmxZUOEVhbbOwe7du/HSSy+hrq4ODz30EF544YVWF3TUfW2dAwAYN24c5s2bh89+9rM444wzUFJSEkSY/d4vf/lLzJo1q9nPvn37/L+50WgU+/bta/Ye0zRRUVEBrTXuvPNOHH300Rg9enQQ4RcMtoGCw3ZPsNjmCQ7bOn2DNSwKSCwWQ2Njo//ccRwYhnHI1xobG5v98aae09Z5yDxfuXIl3njjDaxatYp3NXtBW+fgt7/9LXbv3o0vf/nL2LVrFw4ePIgxY8Zg7ty5QYVbkNo6B2VlZaiursbYsWMBAKeeeio2btyIT3/604HEWqjaOgdbtmzBH//4R6xfvx6RSAQ33HADfvOb3+Azn/lMUOH2W/Pnz8f8+fObrfv3f/93/9g3NjYeMhmUSCSwZMkSRKNRLF++vE9iLWRsAwWH7Z5gsc0THLZ1+gZ7WBSQ448/Hs8++ywA4B//+AfGjx/vv3bEEUfgrbfewieffIJkMom//e1vmDRpUlChFrS2zgMALFu2DIlEAqtXr/a7SFLPauscXHLJJXjsscewZs0afPnLX8asWbP4h7sXtHUORo4cicbGRrz11lsAgL/97W8YN25cIHEWsrbOQTweRygUgm3bUEqhoqICe/fuDSrUgnP88cfjT3/6EwDg2WefxeTJk5u9rrXGV77yFRx55JG47bbboJQKIsyCwjZQcNjuCRbbPMFhW6dvCK21DjoI6hmZSrVbt26F1hp33HEHNm/ejP379+Oiiy7yK2RrrTFv3jx8/vOfDzrkgtTWeaipqcG8efNwwgkn+HcYLrnkEsyYMSPgqAtLe/8tZDz22GP417/+xYrZvaC9c/DXv/4V3/3ud6G1xqRJk7B06dKgQy447Z2Dn//853j00UdhmiaqqqqwYsUKWJYVdNgF4cCBA/ja176GXbt2wTRNfPe730VlZSUeeughVFVVwXEcXHfddTjuuOP891x33XW8iO4GtoGCw3ZPsNjmCQ7bOn2DCQsiIiIiIiIiyjscEkJEREREREREeYcJCyIiIiIiIiLKO0xYEBEREREREVHeYcKCiIiIiIiIiPIOExZERERERERElHeYsCAiIiIiIiKivMOEBRERERERERHlHSYsiIiIiIiIiCjvMGFBRERERERERHmHCQsiIiIiIiIiyjtMWBARERERERFR3mHCgoiIiIiIiIjyDhMWRERERERERJR3mLAgIiIiIiIiorzDhAVRC//4xz+wcOFCzJ49G7NmzcLll1+Of/7znwCAV199FVdffTUA4KabbsIPf/hDAMCRRx6Jjz/+uE/iW7Rokf9Zv/zlL/HTn/60U+/fsGEDamtrMWfOHJx//vmYM2cO5s6di2eeeQYAsGrVKtx2222diqOzrrjiCrz++uut9jN9+nS8+uqrXdpnR3z729/GGWecgTlz5mDOnDm45pprDrldOp3GQw89hLlz52LOnDk499xzsXLlSiSTSQDNz31XdOfYERFR/8E2ReG2KV577TUsXLgQ559/PubOnYuNGzcecju2KYi6xwg6AKJ8kkwm8W//9m/40Y9+hIkTJwIAnnjiCVxxxRVYv349jjnmGHz/+98PNMbnn3/ef1xfX49x48Z1eh9VVVV44okn/OdbtmzBxRdfjPXr13cpjs568MEHe2Q/nfXSSy/h7rvvxvHHH9/mdrfeeiv27NmDH//4x4jH49i/fz+uv/56fP3rX8fKlSu7HUdffmciIgoG2xSF26Y4cOAALrvsMnzzm9/E6aefjqeffhrXX389fvvb37balm0Kou5hDwuiHAcOHMC+ffuwf/9+f915552HW265Bel0Ghs2bMCsWbMO+d5Vq1Zh7ty5mD59erM7FPfddx/OPfdczJ49G1dffTV27doFAFi4cGGzP2y5z7dt24ZFixb52fhHHnkEAHDzzTcDAL74xS/i8ccfxzPPPIP/+q//8j/v/vvvxwUXXIA5c+bgK1/5Cnbu3Nmh7z1hwgSEQiG89957zdb/85//9O8MnXfeeXj88cdbxbFjxw5/+927d2PSpEn+8Vu2bBm+8IUv+K+fffbZ2LZtm3/X41D7+cUvfoG5c+fijDPOwPe+971Dxjt9+nSsWrUKdXV1mDZtGu655x4AwF/+8he/90Tuz3PPPYdkMonNmzfjBz/4AWbPno2vfvWr2L59e6t9v/vuu/jVr36FO+64A/F4HAAQiUTwjW98A2eddVar7VveCcs8b2xsxNVXX405c+bgggsuwNKlS+E4TqvvvHPnTlx11VWYO3cuZs+ejQceeMCP4/TTT8eiRYswc+ZMfPDBB4c8FkRElJ/YpijcNsXzzz+PkSNH4vTTTwcAnHnmmf77crFNQdR97GFBlKO0tBQ33HADLr/8cgwcOBDHH388pkyZgs9+9rOwLKvN944cORLLly/H5s2bcdFFF2HBggV48skn8dxzz+GRRx5BJBLBqlWr2u36l0qlcPXVV+M73/kOJk6ciH379uGiiy7C2LFj8a1vfQuPPfYYfvzjH6OiogIvvPACxo0bh89//vN4/PHHsXXrVvzyl7+EYRj4xS9+gaVLlza783A4v//97yGlxNixY/HHP/7Rj2Px4sW48cYbcfbZZ2Pnzp2YP38+qqurW8WRUV5ejmOOOQYbNmzAtGnTsGHDBjQ0NKCxsRE7duyAYRg44ogj/O0PtR/btvHYY49h165dmD59Oj73uc9h6NChrWLev38/fvazn2Hnzp2YMWMG5s2bh5NPPrnZXZ5c77zzDk466SRcc801GDduHH74wx/iK1/5Cv7v//2/EEL4223atAljx45FLBZr9v7KykrMnDmz3WOZ8dRTT6GxsRFPPPEE0uk0li9fjnfeeafVd77kkkvwpS99CdOnT0cikcAVV1yBqqoq1NbW4v3338d3v/tdnHDCCR3+XCIiyg9sUxRum+LBBx9EZWUllixZgi1btqCkpAQ33HBDq+3YpiDqPiYsiFq49NJLMX/+fLz44ot48cUX8eCDD+LBBx/070gcTuYuyVFHHYVkMomGhgY8++yzmDt3LiKRCADgkksuwQMPPOCPWzyUN998E2+//TaWLFnirzt48CA2b96M44477rDv+8Mf/oBXX30V8+bNAwA4joMDBw4cctu3334bc+bMAeA2IoYMGYLVq1cjHA43iyORSODss88GAAwePBhnn302nnvuOUyaNOmwccyYMQPPPvssqqqqMHjwYIwfPx4vvvgiXnvtNX9fbckcx8rKSgwcOBAfffTRIRsXZ555ph/XgAEDsGfPHrzzzju48847W217/fXX49RTT23W0LrsssuwevVqvPvuuxg5cqS/XkoJx3HajbM9kydPxve+9z0sXLgQJ598Mr74xS+iurq62Tb79+/Hiy++iD179uDee+/1123ZsgW1tbUwDKPNc05ERPmNbYpsHIXUpkilUvjTn/6En/zkJzj22GPx9NNP48tf/jL+8Ic/NEtGsU1B1H1MWBDlqK+vx0svvYTLL78c06ZNw7Rp03Dddddh1qxZeP7551FeXn7Y9xqG+59T5m691hqO4zS7e+84DlKplP9ca+0/bmpqAuAWZ4rH482y+h9++KHflfBwHMfB5Zdfjrq6OgDu2Nk9e/YcctuW400PJZ1ON4s9E29u/IcyY8YMfP7zn8eoUaMwdepUlJSU4M9//jNeffVVfOMb32jzvUD2OALuscw9Rrls2261XVt3Q7Zs2YItW7bg/PPPb/Z9TNNstl1tbS3+9a9/oaGhodkdkZ07d+KWW25pc7xxbqNx5MiReOqpp7Bhwwa88MILuPTSS3Hbbbdh+vTp/jaO40BrjbVr1/oNu48//hi2bWP37t2wLKvZ8SAiov6DbYqsQmtTfPDBBzjiiCNw7LHHAgDOOussLF26FO+8806zXh9sUxB1H2tYEOWoqKjA/fffj7/97W/+ul27dqGhoQHjx4/v9P5OPfVUPProo/74yzVr1uBTn/oULMtCRUWFX1H69ddfx2uvvQYAGD16NEKhkP9HcseOHZg1a5a/rVLK/wOf+/iUU07BI488goaGBgDAvffeixtvvLErhwEAMGbMGBiGgd///vcA3D+uv/vd73DyySe3+uxcQ4YMQXl5OdauXYupU6filFNOwe9//3t88sknmDBhQqvtD7efnialxDe/+U288847AICf/exnOPLIIzFkyJBm2w0ePBizZ8/GkiVL/GPZ0NCAW2+9FWVlZQiFQs22r6io8KuQ//rXv/bX/+xnP8PNN9+MU045BTfccANOOeUUbN68GUD2O8diMRx33HF46KGHAAB79+7tdKEyIiLKT2xTZBVam+K0007Du+++6x/HF198EUIIjBgxotl2bFMQdR/TbEQ5Ro8ejfvuuw/f+9738P7778O2bcTjcdxxxx0YM2aMX9yqoy688ELs2LED8+fPh+M4qK6uxl133QUAWLx4MW666Sb86U9/wpgxY/wxhZZlYfXq1fjmN7+JH/zgB0ilUviP//gPTJ48GQBwzjnnYOHChVi1ahVOO+00fPvb3wbgTuu1c+dOLFiwAEIIDB061H+tK0zTxOrVq3H77bdj1apVSKfTuOqqq3DSSSe1iqNlw2vGjBn40Y9+hKOPPhpSSoRCoUMWl2q5n940fvx4LF26FIsXL0Y6ncaQIUNw9913H3Lb5cuXY/Xq1fjc5z4HpRSSySTOOussfPWrX2217dKlS3HbbbehpKQEJ598MiorKwEA559/Pv77v/8b5557LsLhMIYOHYqFCxcCaP6d77rrLqxYsQKzZ89GMpnErFmzcN555+Hdd9/tvYNBRES9jm2KrEJrU1RWVuK+++7DN77xDRw4cACWZWHVqlXNempksE1B1D1CH65vFBERERERERFRQDgkhIiIiIiIiIjyDhMWRERERERERJR3mLAgIiIiIiIiorwTWNFNx3HQ2NgI0zRbTXNERERE+UtrjaamJkSjUUiZH/c+2K4gIiLqf9prUwSWsGhsbMTWrVuD+ngiIiLqpvHjxyMejwcdBgC2K4iIiPqzw7UpAktYmKYJwA3MsqygwuiQjRs3oqamJugwigqPeTB43IPRq8f9lFPc5Z//3Dv778f4+951yWQSW7du9f+W54P+1K4oFPxvqH/gecp/eXuO2IZoJm/PUz/XXpsisIRFprumZVmHnLM43/SH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BBFmUcn2mT/zzDPYsWMHLrroImzbtg379u3DyJEjMX369KDCLRrZPvfy8nIMHz4chxxyCABg0qRJqKurwzHHHBNIrET5iN/ThYHf6/mP9YDCwHpD/unVLSxaM378ePzjH/8AAKxcuRI1NTUZr2ut8f3vfx+HHnoobrzxRiilggizaIwfPx4rV64EALz++uuoqqryXzv44IOxYcMG7Ny5E/F4HK+++irGjRsXVKhFJdvnDgALFy5EY2Mjli5d6jchpa7J9plfcMEFeOKJJ7Bs2TJcdNFFmDp1Kisp3STb5z5s2DA0NDRgw4YNAIBXX30Vo0aNCiROonzF7+nCwO/1/Md6QGFgvSH/CK21DjqIfLJ3715ce+212LZtG0zTxB133IEBAwbgwQcfRGVlJWzbxpVXXomxY8f6+1x55ZX8gu4kbyTetWvXQmuNW265Be+88w727NmDc845xx99XGuNGTNm4Lzzzgs65KKQ7XOvrq7GjBkzMGHCBP8OzAUXXIBTTjkl4KgLW1u/654nnngCH3zwAUcH7yZtfe4vvfQS7rjjDmitMW7cOMyfPz/okInyCr+nCwO/1/Mf6wGFgfWG/MOEBRERERERERHlHXYJISIiIiIiIqK8w4QFEREREREREeUdJiyIiIiIiIiIKO8wYUFEREREREREeYcJCyIiIiIiIiLKO0xYEBEREREREVHeYcKCiIiIiIiIiPIOExZERERERERElHeYsCAiIiIiIiKivMOEBRERERERERHlHSYsiIiIiIiIiCjvMGFBRERERERERHmHCQsiIiIiIiIiyjtMWBARERERERFR3mHCgqiZ119/HbNnz8bpp5+OqVOn4rvf/S7ee+89AMBbb72Fyy67DABw3XXX4f777wcAHHroofj88897JL45c+b47/X73/8e//Vf/9Wh/VetWoUxY8Zg2rRpOPPMMzFt2jRMnz4dzz//PABgyZIluPHGGzsUR0d973vfw/vvv9/iOCeeeCLeeuutTh2zLU8++SSmTZvm/5x44ok44ogj8Nlnn7XYNplM4sEHH8T06dMxbdo0nHbaaVi8eDHi8TiAzHPfGV357IiIqHCwTlGcdQoA+Pvf/47TTz8d06ZNwwUXXICPPvqo1e1YpyDqGiPoAIjySTwex//9v/8XDzzwAI444ggAwFNPPYXvfe97WLFiBY488kjcddddgcb44osv+s9ra2sxatSoDh+jsrISTz31lL+8Zs0anHvuuVixYkWn4uioe++9t1uO0xFnnnkmzjzzTABAU1MTzj//fFx00UXo379/i20XLVqEL774Ag8//DBKS0uxZ88eXH311fjRj36ExYsXdzmWniozEREFh3WK4q1T7Nu3D9dccw2eeuopDB8+HA899BBuvvlm/OpXv2qxLesURF3DFhZEafbu3Yvdu3djz549/rozzjgDCxYsQDKZxKpVqzB16tRW912yZAmmT5+OE088MeMOxd13343TTjsNp59+Oi677DJs27YNADB79mw888wz/nbpy+vWrcOcOXP8bPxjjz0GAPjhD38IAPj2t7+NJ598Es8//zweeugh//1++ctf4qyzzsK0adPw/e9/H1u2bGlXuUePHo1wOIxPP/00Y/17773n3xk644wz8OSTT7aIY9OmTf72O3bswLhx4/zPb+HChTj//PP910899VSsW7fOv+vR2nEeeeQRTJ8+HV/96lfxs5/9rNV4TzzxRCxZsgSzZs3C5MmTceeddwIA/t//+38ZrSi8n//5n//J2P/ee+9FRUUFvvWtb7U49ieffII//vGPuOWWW1BaWgoAKCkpwQ033ICTTz65xfbN74R5yw0NDbjsssswbdo0nHXWWZg/fz5s225R5i1btuCSSy7B9OnTcfrpp+Oee+7x4zjhhBMwZ84cTJkyBVu3bm31syAiovzEOkXx1imSySS01ti9ezcAoKGhAaFQqMWxWacg6gaaiDI88MADesyYMfrEE0/UV199tf7973+v9+zZo7XW+uWXX9bf+MY3tNZaX3vttfq+++7TWmtdVVWl77//fq211m+//baurq7W8XhcP/bYY/qcc87RDQ0NWmut77rrLj1nzhyttdbnn3++/utf/+q/r7fc1NSkTzvtNF1XV6e11nrXrl3661//ul69erX/Xtu3b28Rwx/+8Ad9+eWX66amJq211suXL9ff/e53W5QvvQyeZ599Vh977LF6z549+q677tI33HCDbmpq0ieddJJ+9tlntdZab968WU+aNEm/9tprLeJIN3v2bP38889rrbU+9dRT9bHHHqvr6+v1e++9p7/+9a9rrbWePHmyfvPNN1scZ/LkyfrGG2/UWmu9detWXV1drTdu3NjiPSZPnqxvu+02P64jjzxSf/TRRy22a8327dv1hAkT9rv9M888o2fMmJH1GM3Pffrn4C3/4Q9/8M91IpHQP/rRj/T69etb7DN79my9YsUKrbXW+/bt07Nnz9Z//vOf9ccff6yrqqr0K6+80q5yERFR/mGdonjrFH/4wx/0EUccoSdOnKiPOeYY/zs+HesURF3HLiFEzVx44YU4++yz8corr+CVV17Bvffei3vvvde/I7E/3l2Sww47DPF4HPX19Vi5ciWmT5+OkpISAMAFF1yAe+65x++32Jr169fjo48+wrx58/x1+/btwzvvvIOxY8fud78XXngBb731FmbMmAEAsG0be/fubXXbjz76CNOmTQMAJBIJDBo0CEuXLkUkEsmIo7GxEaeeeioAYODAgTj11FPxP//zPxg3btx+4zjllFOwcuVKVFZWYuDAgaiqqsIrr7yCd9991z9WNt7nOGDAAPTv3x/bt2/H4MGDW2x30kkn+XH169cPX3zxBT7++GPcfvvtLba9+uqrMWnSJADAo48+ipNOOgnDhg1r9f2llLBtu80421JTU4Of/exnmD17No499lh8+9vfxvDhwzO22bNnD1555RV88cUX+PnPf+6vW7NmDcaMGQPDMLKecyIiym+sU6TiKKY6xQEHHIC7774bf/nLX1BZWYlf//rX+Ld/+zc89dRTEEL427JOQdR1TFgQpamtrcXq1avx3e9+F5MnT8bkyZNx5ZVXYurUqXjxxRfRt2/f/e5rGM4/J++LSmsN27Yzvrhs20YikfCXtdb+86amJgDO4EylpaUZ/UE/++wzvynh/ti2je9+97uYNWsWAKfv7BdffNHqts37m7YmmUxmxO7Fmx5/a0455RScd955OOiggzBx4kSUlZXhn//8J9566y3ccMMNWfcFUp8j4HyW6Z9RuvSml952xx57bJvl+stf/oL58+fv9/UxY8bggw8+QH19PWKxmL9+y5YtWLBgQdb+xumVxmHDhuHvf/87Vq1ahZdffhkXXnghbrzxRpx44on+NrZtQ2uN5cuX+xW7zz//HKFQCDt27IBlWRmfBxERFQ7WKVKKrU5x//33Y/z48aisrAQAnHfeebj11luxY8cOVFRU+NuxTkHUdRzDgihNRUUFfvnLX+LVV1/1123btg319fWoqqrq8PEmTZqExx9/3O9/uWzZMnz5y1+GZVmoqKhAXV0dAOD999/Hu+++CwAYMWIE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qK2tDToEouK0eLHzyMoBERUQKQUOH1QedBjdqra2FuURK+gwiILDOgn1Et2asLBtG4sWLcK7774Ly7Jw8803Y/jw1udmJiIiItof1imIiIioW6cceO655xCPx/HII4/gqquuwm233dadhyciIqJegnUKIiIi6taERW1tLSa5U+yMHTsWdXV13Xl4IiIi6iVYpyAiIqJu7RJSX1+PWCzmLyulkEgkYBj7f5ugKiDFPs4Dy1fYir18QGGWsToeBwDUtSP2QixfR7B8hS/fy9iZOgXQffWKfP98iOeoEPAc5U5H6iRt4XnKf735HHVrwiIWi6GhocFftm17vxUL7Y7+XFVVBcvq2UGT6urqUF1d3aPv2ZNYvsJW7OUDCriMBzoD7LYVe8GWr51YvsLX1TLG43GsXbvW/y7PhY7UKYDurVf0ht+BQsdzlP94jnKsnXWStvA85b9iP0dt1SmE7sbaxrPPPosXXngBt912G15//XX84he/wH333dfqtrt378batWu7662JiIioh1VVVaG0tDQnx+5InQJgvYKIiKiQ7a9O0a0JC29Eby9Dcsstt+Dggw/e77YNDQ0wTZPzYBMRERUQrTWampoQjUYhZbcOh+XrSJ3C2571CiIiosLSVp2iWxMWRERERERERETdITe3RYiIiIiIiIiIuoAJCyIiIiIiIiLKO0xYEBEREREREVHeYcKCiIiIiIiIiPLO/ic0LxL79u3DNddcg+3btyMajeL2229HRUVFi+0+//xzfOtb38If//hHhEKhACLtGG/09HfffReWZeHmm2/G8OHD/deff/553H333TAMAzNmzMDMmTMDjLbj2iofAOzduxcXXnghfvzjH2cdOT5ftVXGP/3pT3j44YehlEJVVRUWLVqUs9H4c6Gt8j377LP41a9+BSEEzjnnHJx99tkBRttx7fkdBYAFCxagT58+uPrqqwOIsvPaKt+DDz6Ixx57zP97esMNN2DkyJFBhdspbZXxzTffxG233QatNQYMGIDFixcXxPeDJ1v5tm3bhiuvvNLf9l//+heuuuoqnHvuuUGFG6j21BUeeugh/PnPfwYAnHDCCbj00kuDCLXXKfb6TjEo9vpMMSj2OksxKPY6SZfoIvfAAw/ou+66S2ut9Z/+9Cd90003tdhm5cqVetq0aXrcuHF63759PR1ipzz77LP62muv1Vpr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
"
class="
"
>
</div>

</div>

</div>

</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell   ">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&nbsp;[8]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
     <div class="CodeMirror cm-s-jupyter">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># looking at the graphs above we decide to use a n = 5 cluster</span>
<span class="n">kmeans</span> <span class="o">=</span> <span class="n">KMeans</span><span class="p">(</span><span class="n">n_clusters</span><span class="o">=</span><span class="mi">5</span><span class="p">,</span> <span class="n">random_state</span><span class="o">=</span><span class="mi">42</span><span class="p">)</span>
<span class="n">cluster_labels</span> <span class="o">=</span> <span class="n">kmeans</span><span class="o">.</span><span class="n">fit_predict</span><span class="p">(</span><span class="n">df_standardized_sliced</span><span class="p">)</span>
<span class="n">df_standardized_sliced</span><span class="p">[</span><span class="s2">&quot;clusters&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">cluster_labels</span>

<span class="c1"># using PCA to reduce the dimenionality to two dimenions (to be able to plot the data with *seaborn*)</span>
<span class="n">pca</span> <span class="o">=</span> <span class="n">PCA</span><span class="p">(</span><span class="n">n_components</span><span class="o">=</span><span class="mi">2</span><span class="p">,</span> <span class="n">whiten</span><span class="o">=</span><span class="kc">False</span><span class="p">,</span> <span class="n">random_state</span><span class="o">=</span><span class="mi">42</span><span class="p">)</span>
<span class="n">authors_standardized_pca</span> <span class="o">=</span> <span class="n">pca</span><span class="o">.</span><span class="n">fit_transform</span><span class="p">(</span><span class="n">df_standardized_sliced</span><span class="p">)</span>
<span class="n">df_authors_standardized_pca</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">DataFrame</span><span class="p">(</span><span class="n">data</span><span class="o">=</span><span class="n">authors_standardized_pca</span><span class="p">,</span> <span class="n">columns</span><span class="o">=</span><span class="p">[</span><span class="s2">&quot;pc_1&quot;</span><span class="p">,</span> <span class="s2">&quot;pc_2&quot;</span><span class="p">])</span>
<span class="n">df_authors_standardized_pca</span><span class="p">[</span><span class="s2">&quot;clusters&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">cluster_labels</span>

<span class="n">df_authors_standardized_pca</span>
</pre></div>

     </div>
</div>
</div>
</div>

<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>


<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt"></div>


<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="application/vnd.jupyter.stderr">
<pre>C:\Users\alexk\AppData\Local\Temp\ipykernel_2952\166135272.py:4: SettingWithCopyWarning: 
A value is trying to be set on a copy of a slice from a DataFrame.
Try using .loc[row_indexer,col_indexer] = value instead

See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
  df_standardized_sliced[&#34;clusters&#34;] = cluster_labels
</pre>
</div>
</div>

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt">Out[8]:</div>



<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/html">
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>pc_1</th>
      <th>pc_2</th>
      <th>clusters</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-1.514660</td>
      <td>0.078953</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-1.633590</td>
      <td>-0.072529</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-1.036557</td>
      <td>-0.358877</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-1.287782</td>
      <td>-0.097219</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2.370543</td>
      <td>2.187308</td>
      <td>2</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>209</th>
      <td>-1.222171</td>
      <td>-0.467485</td>
      <td>0</td>
    </tr>
    <tr>
      <th>210</th>
      <td>2.683152</td>
      <td>0.200280</td>
      <td>3</td>
    </tr>
    <tr>
      <th>211</th>
      <td>0.526099</td>
      <td>-0.195536</td>
      <td>1</td>
    </tr>
    <tr>
      <th>212</th>
      <td>-1.356944</td>
      <td>-0.092281</td>
      <td>0</td>
    </tr>
    <tr>
      <th>213</th>
      <td>-1.514660</td>
      <td>0.078953</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>214 rows × 3 columns</p>
</div>
</div>

</div>

</div>

</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell   ">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&nbsp;[9]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
     <div class="CodeMirror cm-s-jupyter">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Look at our final clustered plot!</span>
<span class="n">sns_plot</span> <span class="o">=</span> <span class="n">sns</span><span class="o">.</span><span class="n">scatterplot</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="s2">&quot;pc_1&quot;</span><span class="p">,</span> <span class="n">y</span><span class="o">=</span><span class="s2">&quot;pc_2&quot;</span><span class="p">,</span> <span class="n">hue</span><span class="o">=</span><span class="s2">&quot;clusters&quot;</span><span class="p">,</span> <span class="n">data</span><span class="o">=</span><span class="n">df_authors_standardized_pca</span><span class="p">)</span>
</pre></div>

     </div>
</div>
</div>
</div>

<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>


<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt"></div>




<div class="jp-RenderedImage jp-OutputArea-output ">
<img src="data:image/png;base64,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uOSSS7j44otZvnz5fp8jbXraL7/8Ms8880yXtnnz5jF+/HgaGxu56aabuO2221IUXf/p7r5PPfVUlixZkqKoksfpdGK1WmOvFUUhGAyiqmnzo9srs2bNoqqqKtVhJJXFYgGif+fXXHMN1113XWoDSiJVVbnlllt4++23+eMf/5jqcPrda6+9Rk5ODkcffTSPP/54qsNJGqPRyKWXXsp5553H1q1bueyyy3jzzTf36/ssbb75zjvvPM4777y49nXr1nH99ddz8803M3ny5BRE1r+6u+9MYbVacblcsdfhcPigT9iZrLa2lquuuooLL7yQM844I9XhJNV9993HjTfeyPe+9z3+85//YDabUx1Sv3n11VfRaDQsXryYb775hltuuYX58+eTn5+f6tD61ZAhQxg0aBAajYYhQ4bgcDhobGykuLi4x+dI62+/jRs3cu211/Lggw8yatSoVIcj+sHhhx/O+++/z6mnnsry5csZMWJEqkMS/aSpqYlLLrmEO++8k6lTp6Y6nKRZsGAB9fX1/OQnP8FkMqHRaA76RwPPPfdc7P/nzJnDXXfdddAnbIBXXnmF9evXc9ddd1FfX4/T6dzv+07rpP3AAw/g9/v59a9/DUR7ZZkwgSOTnHjiiSxatIjZs2cTiUSYN29eqkMS/eTRRx+lo6ODRx55hEceeQSITsg72CcqnXTSSdx6661cdNFFBINBbrvttoyan5NJzj33XG699VYuuOACNBoN8+bN2++RQ6k9LoQQQqSJtJ49LoQQQmQSSdpCCCFEmpCkLYQQQqQJSdpCCCFEmpCkLYQQQqQJSdpCiF5Zt24dp512WqrDECKjSNIWQuy3BQsW8KMf/QiPx5PqUITIKJK0hcggS5Ys4Qc/+AGXXnops2bN4qabbsLv9/P0008za9YsTj31VH73u9/t9RydnZ28++67/P73v09S1EKIXSRpC5Fhli1bxu23386bb76Jz+fj6aef5vnnn+eVV15h4cKFrF69eq+7qdlsNh5++OH9qpcshOgbaV3GVAix/4444ggqKysBOPPMM2ObVNhsNgCefvrpFEYnhNgb6WkLkWF234wiEongdrvRaDSxtvr6ejo6OlIRmhBiHyRpC5Fhli5dSn19PeFwmAULFnDDDTfw4Ycf4nK5CAaD3HDDDXsdHhdCpI4MjwuRYQoKCrj55pupr69n2rRpXHrppVgsFmbPnk04HObEE0/kqKOOSnWYQogEZJcvITLIkiVL+NOf/sSzzz6b6lCEEL0gPW0hRJynn36a119/Pa69oKCAJ554IgURCSFAetpCCCFE2pCJaEIIIUSakKQthBBCpAlJ2kIIIUSakKQthBBCpAlJ2kIIIUSakKQthBBCpIn/B9eZ7Q5XafohAAAAAElFTkSuQmCC
"
class="
"
>
</div>

</div>

</div>

</div>

</div>
<div class="jp-Cell jp-MarkdownCell jp-Notebook-cell">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea"><div class="jp-InputPrompt jp-InputArea-prompt">
</div><div class="jp-RenderedHTMLCommon jp-RenderedMarkdown jp-MarkdownOutput " data-mime-type="text/markdown">
<h3 id="Clustering-Textual-Data">Clustering Textual Data<a class="anchor-link" href="#Clustering-Textual-Data">&#182;</a></h3>
</div>
</div>
</div>
</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell   ">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&nbsp;[10]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
     <div class="CodeMirror cm-s-jupyter">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Get our data from the csv file</span>
<span class="n">df_abstracts</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="s2">&quot;RELIGION_abstracts.csv&quot;</span><span class="p">)</span><span class="o">.</span><span class="n">drop</span><span class="p">(</span><span class="n">columns</span><span class="o">=</span><span class="s2">&quot;Unnamed: 0&quot;</span><span class="p">)</span>
<span class="n">df_abstracts</span><span class="o">.</span><span class="n">describe</span><span class="p">()</span>
</pre></div>

     </div>
</div>
</div>
</div>

<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>


<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt">Out[10]:</div>



<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/html">
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>abstract</th>
      <th>link</th>
      <th>volume</th>
      <th>abstract_lemma</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>701</td>
      <td>701</td>
      <td>701</td>
      <td>701</td>
      <td>701</td>
    </tr>
    <tr>
      <th>unique</th>
      <td>701</td>
      <td>701</td>
      <td>701</td>
      <td>40</td>
      <td>701</td>
    </tr>
    <tr>
      <th>top</th>
      <td>Reinventing the celts</td>
      <td>This is an introductory essay to a special issue on Local and Regional Perspectives on Religion in Western Europe. The introduction seeks to contextualize this special issue in the study of religion in Europe. Based on the articles of the special issue, the article introduces two meso-levels of investigation: regional and local studies, bridging the gap between the national level (the hitherto preferred level of aggregation) and the study of single groups.</td>
      <td>https://www.tandfonline.com/doi/full/10.1080/0048721X.2011.553136</td>
      <td>https://www.tandfonline.com/loi/rrel20?treeId=vrrel20-50</td>
      <td>the prosperity gospel a doctrine in the global Pentecostal Charismatic movement characteristically demonstrate the nexus of the christian faith and wealth this article analyse Mensa Otabil a ghanaian prosperity preacher s 20 year personal development plan for member of his church the International Central Gospel Church ICGC it explore whether or not why and how the member be align their life and vision to his vision of how to achieve a well prosperous community use ethnographic datum obtain from select member of the icgc this article investigate the idea and the implementation of the development plan in order to understand the plan as Otabil s conscious effort to change society through the transformation of individual it argue that Otabil s effort can be analyse as a form of religious engineering where the individual member be invite to act as engineer of their own life and subjectivity</td>
    </tr>
    <tr>
      <th>freq</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>41</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>

</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs  ">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&nbsp;[11]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
     <div class="CodeMirror cm-s-jupyter">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># lemmatization</span>
<span class="kn">import</span> <span class="nn">spacy</span>
<span class="kn">import</span> <span class="nn">re</span>
<span class="n">nlp</span> <span class="o">=</span> <span class="n">spacy</span><span class="o">.</span><span class="n">load</span><span class="p">(</span><span class="s2">&quot;en_core_web_sm&quot;</span><span class="p">)</span>

<span class="k">def</span> <span class="nf">lemmatizeAbstracts</span><span class="p">(</span><span class="n">x</span><span class="p">):</span>
        <span class="n">doc</span> <span class="o">=</span> <span class="n">nlp</span><span class="p">(</span><span class="n">x</span><span class="p">)</span>
        <span class="n">new_text</span> <span class="o">=</span> <span class="p">[]</span>
        <span class="k">for</span> <span class="n">token</span> <span class="ow">in</span> <span class="n">doc</span><span class="p">:</span>
            <span class="n">new_text</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">token</span><span class="o">.</span><span class="n">lemma_</span><span class="p">)</span>
        <span class="n">text_string</span> <span class="o">=</span> <span class="s2">&quot; &quot;</span><span class="o">.</span><span class="n">join</span><span class="p">(</span><span class="n">new_text</span><span class="p">)</span>
        <span class="c1"># getting rid of non-word characters</span>
        <span class="n">text_string</span> <span class="o">=</span> <span class="n">re</span><span class="o">.</span><span class="n">sub</span><span class="p">(</span><span class="sa">r</span><span class="s2">&quot;[^\w\s]+&quot;</span><span class="p">,</span> <span class="s2">&quot;&quot;</span><span class="p">,</span> <span class="n">text_string</span><span class="p">)</span>
        <span class="n">text_string</span> <span class="o">=</span> <span class="n">re</span><span class="o">.</span><span class="n">sub</span><span class="p">(</span><span class="sa">r</span><span class="s2">&quot;\s{2,}&quot;</span><span class="p">,</span> <span class="s2">&quot; &quot;</span><span class="p">,</span> <span class="n">text_string</span><span class="p">)</span>
        <span class="k">return</span> <span class="n">text_string</span>

<span class="n">df_abstracts</span><span class="p">[</span><span class="s2">&quot;abstract_lemma&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">df_abstracts</span><span class="p">[</span><span class="s2">&quot;abstract&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">apply</span><span class="p">(</span><span class="n">lemmatizeAbstracts</span><span class="p">)</span>
<span class="n">df_abstracts</span><span class="o">.</span><span class="n">to_csv</span><span class="p">(</span><span class="s2">&quot;RELIGION_abstracts.csv&quot;</span><span class="p">)</span>
</pre></div>

     </div>
</div>
</div>
</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell   ">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&nbsp;[12]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
     <div class="CodeMirror cm-s-jupyter">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">tfidf</span> <span class="o">=</span> <span class="n">TfidfVectorizer</span><span class="p">(</span><span class="n">stop_words</span><span class="o">=</span><span class="s2">&quot;english&quot;</span><span class="p">)</span>
<span class="n">df_abstracts_tfidf</span> <span class="o">=</span> <span class="n">tfidf</span><span class="o">.</span><span class="n">fit_transform</span><span class="p">(</span><span class="n">df_abstracts</span><span class="p">[</span><span class="s2">&quot;abstract_lemma&quot;</span><span class="p">])</span>
<span class="n">df_abstracts_tfidf</span>
</pre></div>

     </div>
</div>
</div>
</div>

<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>


<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt">Out[12]:</div>




<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/plain">
<pre>&lt;701x8224 sparse matrix of type &#39;&lt;class &#39;numpy.float64&#39;&gt;&#39;
	with 40605 stored elements in Compressed Sparse Row format&gt;</pre>
</div>

</div>

</div>

</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell   ">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&nbsp;[13]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
     <div class="CodeMirror cm-s-jupyter">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># creating a new TF-IDF matrix</span>

<span class="n">tfidf</span> <span class="o">=</span> <span class="n">TfidfVectorizer</span><span class="p">(</span><span class="n">stop_words</span><span class="o">=</span><span class="s2">&quot;english&quot;</span><span class="p">,</span> <span class="n">ngram_range</span><span class="o">=</span><span class="p">(</span><span class="mi">1</span><span class="p">,</span><span class="mi">2</span><span class="p">),</span> <span class="n">max_features</span><span class="o">=</span><span class="mi">250</span><span class="p">,</span> <span class="n">strip_accents</span><span class="o">=</span><span class="s2">&quot;unicode&quot;</span><span class="p">,</span> <span class="n">min_df</span><span class="o">=</span><span class="mi">10</span><span class="p">,</span> <span class="n">max_df</span><span class="o">=</span><span class="mi">200</span><span class="p">)</span>
<span class="n">tfidf_religion_array</span> <span class="o">=</span> <span class="n">tfidf</span><span class="o">.</span><span class="n">fit_transform</span><span class="p">(</span><span class="n">df_abstracts</span><span class="p">[</span><span class="s2">&quot;abstract_lemma&quot;</span><span class="p">])</span>
<span class="n">df_abstracts_tfidf</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">DataFrame</span><span class="p">(</span><span class="n">tfidf_religion_array</span><span class="o">.</span><span class="n">toarray</span><span class="p">(),</span> <span class="n">index</span><span class="o">=</span><span class="n">df_abstracts</span><span class="o">.</span><span class="n">index</span><span class="p">,</span> <span class="n">columns</span><span class="o">=</span><span class="n">tfidf</span><span class="o">.</span><span class="n">get_feature_names_out</span><span class="p">())</span>
<span class="n">df_abstracts_tfidf</span><span class="o">.</span><span class="n">describe</span><span class="p">()</span>
</pre></div>

     </div>
</div>
</div>
</div>

<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>


<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt">Out[13]:</div>



<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/html">
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>academic</th>
      <th>account</th>
      <th>activity</th>
      <th>address</th>
      <th>african</th>
      <th>agency</th>
      <th>aim</th>
      <th>allow</th>
      <th>american</th>
      <th>analyse</th>
      <th>...</th>
      <th>use</th>
      <th>value</th>
      <th>various</th>
      <th>view</th>
      <th>way</th>
      <th>western</th>
      <th>woman</th>
      <th>work</th>
      <th>world</th>
      <th>year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>701.000000</td>
      <td>701.000000</td>
      <td>701.000000</td>
      <td>701.000000</td>
      <td>701.000000</td>
      <td>701.000000</td>
      <td>701.000000</td>
      <td>701.000000</td>
      <td>701.000000</td>
      <td>701.000000</td>
      <td>...</td>
      <td>701.000000</td>
      <td>701.000000</td>
      <td>701.000000</td>
      <td>701.000000</td>
      <td>701.000000</td>
      <td>701.000000</td>
      <td>701.000000</td>
      <td>701.000000</td>
      <td>701.000000</td>
      <td>701.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>0.017407</td>
      <td>0.017756</td>
      <td>0.010633</td>
      <td>0.011059</td>
      <td>0.011356</td>
      <td>0.009061</td>
      <td>0.010451</td>
      <td>0.009127</td>
      <td>0.015210</td>
      <td>0.011713</td>
      <td>...</td>
      <td>0.033074</td>
      <td>0.014268</td>
      <td>0.013633</td>
      <td>0.021310</td>
      <td>0.027744</td>
      <td>0.021257</td>
      <td>0.018406</td>
      <td>0.028048</td>
      <td>0.028877</td>
      <td>0.014563</td>
    </tr>
    <tr>
      <th>std</th>
      <td>0.063839</td>
      <td>0.067667</td>
      <td>0.051894</td>
      <td>0.047114</td>
      <td>0.065659</td>
      <td>0.053946</td>
      <td>0.045080</td>
      <td>0.042445</td>
      <td>0.068153</td>
      <td>0.051143</td>
      <td>...</td>
      <td>0.074190</td>
      <td>0.061468</td>
      <td>0.052642</td>
      <td>0.064568</td>
      <td>0.062593</td>
      <td>0.078245</td>
      <td>0.095377</td>
      <td>0.074917</td>
      <td>0.073751</td>
      <td>0.052971</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>...</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>...</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>...</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>...</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>0.493789</td>
      <td>0.709637</td>
      <td>0.509307</td>
      <td>0.360085</td>
      <td>0.737092</td>
      <td>0.658383</td>
      <td>0.359469</td>
      <td>0.409185</td>
      <td>0.617276</td>
      <td>0.457299</td>
      <td>...</td>
      <td>0.609089</td>
      <td>0.828761</td>
      <td>0.534004</td>
      <td>0.515410</td>
      <td>0.364839</td>
      <td>0.724760</td>
      <td>0.941362</td>
      <td>0.604694</td>
      <td>0.492094</td>
      <td>0.365748</td>
    </tr>
  </tbody>
</table>
<p>8 rows × 250 columns</p>
</div>
</div>

</div>

</div>

</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell   ">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&nbsp;[14]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
     <div class="CodeMirror cm-s-jupyter">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># using PCA to reduce the dimensionality</span>
<span class="n">pca</span> <span class="o">=</span> <span class="n">PCA</span><span class="p">(</span><span class="n">n_components</span><span class="o">=</span><span class="mi">10</span><span class="p">,</span> <span class="n">whiten</span><span class="o">=</span><span class="kc">False</span><span class="p">,</span> <span class="n">random_state</span><span class="o">=</span><span class="mi">42</span><span class="p">)</span>
<span class="n">abstracts_pca</span> <span class="o">=</span> <span class="n">pca</span><span class="o">.</span><span class="n">fit_transform</span><span class="p">(</span><span class="n">df_abstracts_tfidf</span><span class="p">)</span>
<span class="n">df_abstracts_pca</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">DataFrame</span><span class="p">(</span><span class="n">data</span><span class="o">=</span><span class="n">abstracts_pca</span><span class="p">)</span>
<span class="n">df_abstracts_pca</span>
</pre></div>

     </div>
</div>
</div>
</div>

<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>


<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt">Out[14]:</div>



<div class="jp-RenderedHTMLCommon jp-RenderedHTML jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/html">
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
      <th>7</th>
      <th>8</th>
      <th>9</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-0.087536</td>
      <td>-0.133754</td>
      <td>-0.019252</td>
      <td>-0.127524</td>
      <td>0.188059</td>
      <td>0.079132</td>
      <td>-0.014340</td>
      <td>-0.032934</td>
      <td>0.239940</td>
      <td>-0.081444</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-0.100590</td>
      <td>-0.184206</td>
      <td>-0.063085</td>
      <td>-0.169670</td>
      <td>0.244982</td>
      <td>0.102516</td>
      <td>-0.014914</td>
      <td>-0.090813</td>
      <td>0.278014</td>
      <td>-0.161025</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-0.135874</td>
      <td>-0.110891</td>
      <td>-0.008002</td>
      <td>-0.064511</td>
      <td>0.363380</td>
      <td>0.108146</td>
      <td>-0.041419</td>
      <td>-0.082428</td>
      <td>0.291033</td>
      <td>-0.168784</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-0.107712</td>
      <td>-0.138008</td>
      <td>-0.056803</td>
      <td>-0.137601</td>
      <td>0.269000</td>
      <td>0.133273</td>
      <td>-0.044879</td>
      <td>-0.071159</td>
      <td>0.271787</td>
      <td>-0.106355</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-0.011910</td>
      <td>-0.151941</td>
      <td>0.018459</td>
      <td>-0.185845</td>
      <td>0.245275</td>
      <td>0.103453</td>
      <td>0.064013</td>
      <td>-0.073901</td>
      <td>0.214777</td>
      <td>-0.032233</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>696</th>
      <td>0.172567</td>
      <td>-0.003118</td>
      <td>0.147293</td>
      <td>0.031122</td>
      <td>0.175650</td>
      <td>0.071933</td>
      <td>0.056937</td>
      <td>-0.038804</td>
      <td>-0.070862</td>
      <td>0.024917</td>
    </tr>
    <tr>
      <th>697</th>
      <td>-0.034094</td>
      <td>-0.003756</td>
      <td>0.008462</td>
      <td>-0.112967</td>
      <td>-0.038806</td>
      <td>0.000519</td>
      <td>-0.075537</td>
      <td>-0.050137</td>
      <td>-0.048811</td>
      <td>0.128039</td>
    </tr>
    <tr>
      <th>698</th>
      <td>0.005142</td>
      <td>0.090452</td>
      <td>0.043544</td>
      <td>0.103490</td>
      <td>-0.047075</td>
      <td>0.061992</td>
      <td>0.008298</td>
      <td>-0.046505</td>
      <td>-0.026135</td>
      <td>-0.148307</td>
    </tr>
    <tr>
      <th>699</th>
      <td>-0.060472</td>
      <td>-0.051475</td>
      <td>0.036484</td>
      <td>0.050968</td>
      <td>0.112632</td>
      <td>0.022258</td>
      <td>-0.148895</td>
      <td>-0.055882</td>
      <td>0.104067</td>
      <td>-0.052197</td>
    </tr>
    <tr>
      <th>700</th>
      <td>0.018514</td>
      <td>-0.032739</td>
      <td>-0.130765</td>
      <td>0.108108</td>
      <td>-0.088974</td>
      <td>-0.034801</td>
      <td>-0.120599</td>
      <td>0.107453</td>
      <td>0.054444</td>
      <td>0.008300</td>
    </tr>
  </tbody>
</table>
<p>701 rows × 10 columns</p>
</div>
</div>

</div>

</div>

</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell   ">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&nbsp;[15]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
     <div class="CodeMirror cm-s-jupyter">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">elbowPlot</span><span class="p">(</span><span class="nb">range</span><span class="p">(</span><span class="mi">10</span><span class="p">,</span><span class="mi">100</span><span class="p">),</span> <span class="n">df_abstracts_pca</span><span class="p">,</span> <span class="n">figsize</span><span class="o">=</span><span class="p">(</span><span class="mi">20</span><span class="p">,</span><span class="mi">20</span><span class="p">))</span>
</pre></div>

     </div>
</div>
</div>
</div>

<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>


<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt"></div>


<div class="jp-RenderedText jp-OutputArea-output" data-mime-type="application/vnd.jupyter.stderr">
<pre>C:\Users\alexk\AppData\Local\Temp\ipykernel_2952\2335342308.py:38: UserWarning: Matplotlib is currently using module://matplotlib_inline.backend_inline, which is a non-GUI backend, so cannot show the figure.
  fig.show()
</pre>
</div>
</div>

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt"></div>




<div class="jp-RenderedImage jp-OutputArea-output ">
<img src="data:image/png;base64,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eqIIAAAA2hChiLelQ11tdhrWN49MfzkvuacIAAAA2gShiLdt3KrXz259ambBSwAAAIB1QSjibXv1nqKpXj8DAACAtkAo4m3bbr0+6VhXm1uEIgAAAGgThCLetoa62uywfp88PH1u5ixeWvQcAAAA4B0SinhHdhveP+VycuuT7ikCAACA1k4o4h1ZfaG1188AAACg9ROKeEd2WL9vGupqXGgNAAAAbYBQxDvSsb4226/XJw9Om5MFy1YWPQcAAAB4B4Qi3rHdhg9IuZw8OHNx0VMAAACAd0Ao4h0bN7xfkuT+mYsKXgIAAAC8E0IR79gO6/dNfW1N7vNEEQAAALRqQhHvWKcOddl+vT6ZPLcpsxctLXoOAAAA8DYJRawTh2wyJM3l5JJHni16CgAAAPA2CUWsE+/bYliS5OIHni50BwAAAPD2CUWsE+v17JzN+zbmxqkvZvp8dxUBAABAayQUsc7ss173lMvJXx96pugpAAAAwNsgFLHO7Llet9SUSvnzA0IRAAAAtEZCEetMn8a67DGif+58ZlaenrOw6DkAAADAWhKKWKfev+pS67886KkiAAAAaG2EItap92y2XupqSvnzg08XPQUAAABYS0IR61SvTg3Zd/SgPPDCnDw+c17RcwAAAIC1IBSxzh2x5bAkycVePwMAAIBWRShinTtkkyHpWFebix54KuVyueg5AAAAwBoSiljnunXskAM3HpxJM+fnkekvFz0HAAAAWENCERVxxKpPP3OpNQAAALQeQhEVceCYwenSUJc/P/C0188AAACglRCKqIhOHepyyCZD89Schbn3udlFzwEAAADWgFBExaz+9LM/P/B0oTsAAACANSMUUTH7jhqYHo0dcvGDT6e52etnAAAAUO2EIiqmQ11t3rPpepk2f0lue2pm0XMAAACAt1CxULRy5cp85StfyZFHHpmjjz46zz77bB577LHsuuuuOfbYY3PsscfmiiuuqNSPp0q8+vqZTz8DAACAqldXqYNvvPHGJMlFF12Uu+++O6effnr23HPPnHDCCfnQhz5UqR9Lldl9eP/069Ixf33omfzs0G1TV+shNgAAAKhWFftv7XvvvXdOO+20JMm0adPSp0+fPProo7npppty9NFH59RTT83ChQsr9eOpEnW1NTl88/Xz0qKlueGJF4ueAwAAALyJUrlcrugtw6ecckquvfba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+dGU9fT50ZS3+xxpytp9fvQ0h93rVfe83edHU9bT50dT3u5zpN3zYfd61TSz3fWYn5+vJ554Qnv37lVYWJieeuopORwOY4+m7C/Pg6lHU/7UqVPGHk3ZwsJCY4+e5jD1aMrn5OQYezRlw8PDbXs05V955RVjj3bPh6lHu5k9vc45b1jwinfeecfq2bOndfPNN1uWZVn33XeftWLFCsuyLGvEiBHWnDlzbLMjR460unfvbg0ZMqTcc2+//XZr8+bNlmVZ1ieffGKNGTPGY/7++++3Vq1aZVmWZQ0dOtTjHJZlWZs3b7b69ev3q9+zy3/22WfWe++997uej6FDh1ozZsywLMuyli9fbi1YsMDjHJZlWceOHbOuvfZa69ChQx7PfuCBB6yFCxdalmVZjzzyiDV//nzb7PXXX2+tXbvWsizLGjdunDV58uTS7BdffGGNGjXKsizLOnLkiNW+fXvbHk3ZrKws66677rI6d+5sTZgw4Vczm/J2XZqydj2aspZl36Mpb9ejKeupR7tZLOu3XZqydj2asp56nDt3rjVs2DDLsixrxYoV1oABA2x7NGU99WjK2/Voynq6Hk15yzJ3acra9WjKeurRbg5Tj6asp+vRlPfUZX5+vvXAAw9Y3bp1s3bs2OHxvuqe9dSje7a8+6p73lOP7lm7Du3ynu6r7llPPZrmsCz7+6p73lOP7llPHZ4+fdrq3bv3r/4uux5NWU89mvJ2XZqynno05S3L3KUpa9ejKeupR7s5LOu3XZqynno05e26XLFihXXfffdZRUVFVnZ2tvXqq6/a9mjKeurRlLfr0ZS169GUtSz769GUt+vRlPXUo90sph5NWbseTVlP12NZzzzzjDVx4kSP91X3rKceTfny7q1ls56uR1PesjzfW8tmPd1X3bOeerSbw7Ls761ls56uR1Persu5c+dagwYNsizLspYsWWI9+OCDHl/nuGfLe53jnvf0Osc9a9ejKWtZ9h2a8p5e57hny3udY5rFssyvc9yzdj2asp6ux/Hjx1vDhw+3LMuydu7cafXv39+2R1PWU4+mvF2Ppqxdj6aspx5NebseTVlPPdrNYurRlLXr0ZT9vffVyu48XH1VDMnJyXrttddKf52enq7WrVtLktq1a6dly5bZZlu2bKlnnnnmd507btw4paSkSDrzX+cDAwM95l977TVdcsklys/P1+HDhxUTE2ObPXr0qF566SWlpaX9rlk2bdqkhQsX6vbbb1daWpqys7Nts999950OHTqkO++8U9OmTSt9bkzZsrPfcccdqlatmsc5UlJSdOzYMVmWpZycHLlcLtvsoUOH1LJlS0lnnve1a9eW/tlVV12lwYMHl/7az8/PtkdTNicnRw899JB69+79m8diytt1acra9WjKeurRlLfr0ZT11KMp/wv3Lk1Zux5NWU89dunSRSNHjpQk7d+/X7GxsbY9mrKeejTl7Xo0ZT1dj6a8XZemrF2PpqynHk15ux5NWU/Xoynvqcvnn39ef/vb30r/Pk/3Vfespx7ds+XdV93znnp0z5Z3X3XPe7qvumc99eie/YXdfdU976lH96ynDrdu3apTp06pf//+6tevn9atW2fboynrqUdT3q5LU9ZTj6a8XZemrF2PpqynHk15uy5NWU89mvJ2XS5ZskT169fXwIEDNWDAAHXo0MG2R1PWU4+mvF2Ppqxdj6asp+vRlLfr0ZT11KMpb9ejKWvXoynr6Xr8xcaNG7Vjxw7deuutHu+r7llPPZry5d1by2Y9XY+mfHn31rJZT/dV96ynHk35X9jdW8tmPV2Pprxdl7Vr11ZRUZGKi4uVnZ0tl8tl26Mp66lHU96uR1PWrkdT1lOHprxdj6aspx5NebseTVm7Hk1ZT9fjjh071K5dO0lSnTp1tHPnTtseTVlPPZrydj2asnY9mrKeejTl7Xo0ZT31aMrb9WjK2vVoyv6e++r5gEWRl3Tv3v1XNxrLsuRwOCRJoaGhOnnypG326quvLs2Wd27Zf0H46KOPdOedd3rM+/n5KSMjQz179tTRo0dVu3ZtY7aoqEhPPvmk0tLSFBoa+rtmadasmf75z3/q448/Vo0aNfTGG2/YZjMyMhQREaEPPvhA8fHxevfdd22z0plva1i+fLluuOGGcuf45csFe/TooaysLF166aW22Ro1amjVqlWSpAULFujUqVOlfxYaGqqwsDBlZ2dr0KBBGjJkiG2PpmyNGjXUvHlz43Nnytt1acra9eieHTx4sMceTWfb9WjKeurRlLfr0pS169HuubbrUZJcLpeGDh2qkSNHqnv37h6vR/espx5NeU/XpHvW0/Xonu/WrZvHLt3P9nQ9umc99WjK2/Voynq6Hu2eb1OXkyZNUnR0tNq2bVv6sXY9mrJ2PZqynjo05e16dM8WFxd77NB0tl2Ppqxdj6asZN+hKW/Xo91zbXc9BgUF6a677tJ7772nZ599Vo899phtj6ZsfHy87fVoykdHR0v6bZd2c9hdj+75Rx55RMOGDTN2aTq7cePGxh5N2T179thej6Z8YWGhsUtTNikpyfZ6NOXtujx69Kg2bdqkV155pdweTdmkpCTbHk35qlWrGns0ZZ1Op7FH9+yjjz6qtLQ02+vRdLbd9WjKerqv2j1/ph5NWbvr0e659vT5UTrz7WoDBw6U5Pn1qnu2vM+P7vnyXrOWzZb3+bFs/ve8Zi17tqfPj+7Z8j4/uuclz69Zy2bL+/zonre7HkNCQpSRkaEePXpoxIgR6tu3r22PpqynHk15ux5NWbse3bN33HGHxw5NZ9v1aMp66tGUt+vRlLXr0e65trseU1JStGDBAlmWVbqot+vRlE1ISLDt0ZT/Zdnj3qMpK8nYo3v2wIEDeuKJJ2x7NJ3dpEkTY4+mrKceTfmioiJjj6ZscnKysUdT9vfcV88HLIrOkbLft5iTk6OIiIizdvbMmTP19NNP65133il9UexJYmKi5syZoz59+ui5554zZtLT07Vnzx4988wzeuSRR7Rjxw6NHj3a47ldu3ZVkyZNSn++efNm22xUVJQ6deokSerUqZM2bdrk8exZs2apZ8+ev/qqFDujR4/Wxx9/rFmzZum6666zfYzSme/jffvtt3XvvfcqJiZGVapU+dWfHzhwQP369VPv3r3Vq1cvjz26Z8tjytt1acra9Vg2W6tWrXJ7dD/bU4/u2fJ6NM1t16V71lOP7tnyepTOfNXD7NmzNWLECOXl5ZX+vul6LJvNzc019ucp7+madM+Wdz3+kh84cKC2bt3qscuyZ1955ZUer8ey2fDw8HKvR/e5PV2TZbOjRo0q93osm3/mmWeMXX755ZdatmyZ+vbtqy1btmjo0KE6cuRI6RllezRlDx8+/NviPGTtOrTLm3p0z/bq1Uvbtm2z7dB0drt27Yw9mrJOp9PYo93Mdh2a8sOGDTP2aMo+8sgjttdj7dq1de2118rhcKh27dqKiopSVlaWsUdT1q5HT3lTl3ZZu+vRPb9//37t3LnT2KXp7LZt2xp7NGXtevQ0t6lLU3bo0KG216Mpb9dlVFSUrrzySgUEBKhOnToKDAz81UKhbI+mbNlr151d3tSjXdbUo3v24MGD2r17t+31aDq7Q4cOxh5N2aKiItse7eY29WjKPvbYY8YeTdm0tDSPnx9PnDihH3/8UZdddpkkz69X3bPlMeXt7q2mrKfPj2Xz5b1mdT/b0+sc92x5r3NMc9vdW92z5b1edc/bvdb54IMPdOWVV2r27NmaMmWKhg0bpoKCgtJzyvZoypZ9TeTOLm/q0S5r6tE9e9ttt3n8/Gg62+7zoynrqUe7uU09mrJ2PZqydq9xJOnGG29UWFiY+vXrpwULFqhx48a216Mp6+nfkezyph7tsqYe3bMOh0N79+617dF0dvfu3Y09mrKeerSb29SjKTt27Fhjj3bZ8v6943zAougcadSokVauXClJ+vbbb9WqVauzcu6UKVP00Ucfafz48apRo0a5+QEDBmj37t2Szmym7d54q1mzZpoxY4bGjx+vcePGqV69enryySc9nn3XXXdpw4YNkqTly5ercePGttnU1FQtWrRIkrR69WrVq1fP49nLly8v/bK/8kRGRiosLEzSmf96deLECdvsokWLNGbMGL3zzjs6duyY2rRpU/pnmZmZ6t+/vx5//HHddNNNkux7NGU9MeXtujRl7Xp0z5bXo+lsux5NWU892j0npi5NWbseTVlPPU6ePFlvv/22JCk4OFgOh0NNmjQx9mjKevrEa8rPnTvX2KMp++CDD9pej+752NhYff3118Yu7c429WjKtm7d2rZHu+fE1KMpGxUVZXs9mvILFy40dvnxxx+XPq8pKSl6/vnn1a5dO2OPpuwvX5HgzpRdtmyZ7X3VlB8xYoSxR/fsjBkzNG/ePNvr0XT2Aw88YOzRlO3YsaOxR7vnw+6+asonJSUZezRl09PTba/HL774ovTF16FDh5Sdna02bdoYezRl7Xq0y69atcrYpSn71FNP2V6P7vlatWpp1qxZxi5NZw8cONDYoynbtWtX2+vR7jkxdWnKJicn216Ppvz69euNXaampmrx4sWyLEuHDh3SqVOndPnllxt7NGWjoqJsezTlv/32W2OPpuyTTz5p7NE9GxcXp+nTp9tej6az7733XmOPpmznzp1te7R7Tkw9mrJ2PZqya9eutb0ef5ntiiuuKP21p9er7tnyuOc9vWZ1z5b3erVsvrzXOu5ne3q96p4t7/Wq6Tmxu7e6Z8t7veqet3utExERUfom9JGRkSosLLTt0ZQtKir6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
"
class="
"
>
</div>

</div>

</div>

</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell   ">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&nbsp;[16]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
     <div class="CodeMirror cm-s-jupyter">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">kmeans</span> <span class="o">=</span> <span class="n">KMeans</span><span class="p">(</span><span class="n">n_clusters</span><span class="o">=</span><span class="mi">100</span><span class="p">,</span> <span class="n">random_state</span><span class="o">=</span><span class="mi">42</span><span class="p">)</span>
<span class="n">abstracts_labels</span> <span class="o">=</span> <span class="n">kmeans</span><span class="o">.</span><span class="n">fit_predict</span><span class="p">(</span><span class="n">df_abstracts_pca</span><span class="p">)</span>

<span class="n">df_abstracts_labeled</span> <span class="o">=</span> <span class="n">df_abstracts</span><span class="o">.</span><span class="n">copy</span><span class="p">()</span>
<span class="n">df_abstracts_labeled</span><span class="p">[</span><span class="s2">&quot;cluster&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">abstracts_labels</span>
<span class="n">df_abstracts_labeled</span><span class="p">[</span><span class="n">df_abstracts_labeled</span><span class="p">[</span><span class="s2">&quot;cluster&quot;</span><span class="p">]</span> <span class="o">==</span> <span class="mi">9</span><span class="p">][</span><span class="s2">&quot;title&quot;</span><span class="p">]</span>
</pre></div>

     </div>
</div>
</div>
</div>

<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>


<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt">Out[16]:</div>




<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/plain">
<pre>80                                    Latin America 1520–1600: a page in the history of the study of religion
120    Stone-agency: sense, sight and magical efficacy in traditions of the Highlands and Islands of Scotland
260         How compatible were Durkheim and Mauss on matters relating to religion? Some introductory remarks
392                                                        Religion and Spirituality in Lonely Planet&#39;s India
427                         Representation and its discontents: Orientalism, Islam and the Palestinian crisis
458                          Religion Within the Limits of History: Schleiermacher and Religion—A Reappraisal
491                      A Tapestry of Kings: Edited Volumes and the Growth of Knowledge in Religious Studies
637                                        The Yogi&#39;s human self: Tāyumānavar in the Tamil mystical tradition
669                                     Rachel&#39;s tomb: Societal liminality and the revitalization of a shrine
673                      The hermeneutics of visionary experience: Revelation and interpretation in the Zohar
Name: title, dtype: object</pre>
</div>

</div>

</div>

</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell   ">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&nbsp;[17]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
     <div class="CodeMirror cm-s-jupyter">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">findOptimalEps</span><span class="p">(</span><span class="mi">2</span><span class="p">,</span> <span class="n">df_abstracts_pca</span><span class="p">)</span>
</pre></div>

     </div>
</div>
</div>
</div>

<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>


<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt"></div>




<div class="jp-RenderedImage jp-OutputArea-output ">
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAe8AAAFXCAYAAACLEMbVAAAAOXRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjUuMSwgaHR0cHM6Ly9tYXRwbG90bGliLm9yZy/YYfK9AAAACXBIWXMAAAsTAAALEwEAmpwYAAAxSElEQVR4nO3deXhU9d338fdkJjNZJvvCFtZAAEFBgrggVEHU8oio6BN8WmirbcVatbdatbeoFCnFujzexdbH1tpW3EDEBatCUeuCAhIJEE3CFnbIvk222c7zR2Q0shgkk8mZ+byuiyvMnJkz32/gyie/3znndyyGYRiIiIiIaUSFugARERE5OQpvERERk1F4i4iImIzCW0RExGQU3iIiIiZjC3UBHeH3+2lsbCQ6OhqLxRLqckRERILOMAw8Hg/x8fFERbUfa5sivBsbG9m2bVuoyxAREelyOTk5JCQktHvOFOEdHR0NtDVgt9s7ZZ+FhYWMHDmyU/bVnanP8KI+w4v6DC+d3afb7Wbbtm2BDPw6U4T3kalyu92Ow+HotP125r66M/UZXtRneFGf4SUYfR7rcLFOWBMRETEZhbeIiIjJKLxFRERMRuEtIiJiMgpvERERk1F4i4iImIzCW0RExGQU3iIiIiaj8BYRETEZhbeIiMgpOlTfxOrddRiG0SWfp/AWERE5RY+9X8Tcjw+wo7KhSz5P4S0iInKKXG4vAB6fv0s+T+EtIiJyio6Ets3aNbGq8BYRETlFXn/bse7oqKPvABYMCm8REZFT5PV/OfKO0shbRETEFL6aNtfIW0RExBSOTJtr5C0iImIS3i9H3tFmP2HN7/dz3333kZeXx6xZs9izZ88xX3fvvffy8MMPB6sMERGRoPtq5G3yafM1a9bgdrtZunQpt99+O4sWLTrqNS+++CLbtm0LVgkiIiJdInDM2+zT5vn5+UyYMAGA0aNHU1hY2G77pk2b2Lx5M3l5ecEqQUREpEv4jlwq1kUnrNmCtWOXy4XT6Qw8tlqteL1ebDYb5eXlPP744zz++OO89dZbHd7nN38BOFX5+fmdur/uSn2GF/UZXtRneKiprwdg02efYbEEP8CDFt5Op5PGxsbAY7/fj83W9nFvv/02NTU1/PznP6eiooKWlhYGDRrEVVdddcJ9jhw5EofD0Sn15efnk5ub2yn76s7UZ3hRn+FFfYaPmLUVWC1NjB07ttP22draetxBa9DCe8yYMbz33ntMnTqVgoICcnJyAttmz57N7NmzAVixYgW7du361uAWERHprrx+f5edrAZBDO8pU6awdu1aZs6ciWEYLFy4kJUrV9LU1KTj3CIiEla8fgNbF0yXHxG08I6KimL+/PntnsvOzj7qdRpxi4iI2Xl8frroEm9Ai7SIiIicMq/fj7ULR94KbxERkVPk9Rtdesxb4S0iInKKNPIWERExGY/P0DFvERERM+nqS8UU3iIiIqfI6zM0bS4iImImHr+fLlrWHFB4i4iInDKv349V0+YiIiLm4fV17QprCm8REZFT5PXrbHMRERHT8PsN/IZG3iIiIqbh9fsBdKmYiIiIWXj9BoAuFRMRETELj69t5K1j3iIiIiahkbeIiIjJ6Ji3iIiIyQSmzbXCmoiIiDkEps018hYRETEHTZuLiIiYjNenE9ZERERMxXNk5K1j3iIiIuYQGHlr2lxERMQcdMxbRETEZHSpmIiIiMlohTURERGT0bS5iIiIyXgCJ6x13WcqvEVERE7BkZG3ps1FRERM4sgxb02bi4iImIRG3iIiIiYTuFRMx7xFRETMITBtrpG3iIiIORxZHlXHvEVEREzC49cKayIiIqaiE9ZERERMxqdpcxEREXMJjLwV3iIiIuYQWB5Vx7xFRETMQce8RURETEbLo4qIiJiMVlgTERExmcD9vDVtLiIiYg6aNhcRETGZwLS5zjYXERExhyMjb13nLSIiYhI65i0iImIyR+4qppG3iIiISeiuYiIiIibj9WltcxEREVMJXCqmY94iIiLmEJg21wprIiIi5nDkhDWNvEVEREwicKmYjnmLiIiYw1crrCm8RURETKGm2U2c3Up0F14rpvAWERE5BVWNraTFObr0MxXeIiIip6CqKYzC2+/3c99995GXl8esWbPYs2dPu+2rVq1ixowZXH311bz00kvBKkNERCRo3F4frlYvafFdG962YO14zZo1uN1uli5dSkFBAYsWLeKJJ54AwOfz8cgjj/Dyyy8TFxfH1KlTmTx5MqmpqcEqR0REpNNVNbUCkNrFI++ghXd+fj4TJkwAYPTo0RQWFga2Wa1W3nzzTWw2G1VVVQDEx8cHqxQREZGgqGpsC++uHnkHbdrc5XLhdDoDj61WK16vN/DYZrOxevVqpk+fztixY7HZgvZ7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
"
class="
"
>
</div>

</div>

</div>

</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell   ">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&nbsp;[18]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
     <div class="CodeMirror cm-s-jupyter">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">dbscan</span> <span class="o">=</span> <span class="n">DBSCAN</span><span class="p">(</span><span class="n">eps</span><span class="o">=</span><span class="mf">0.2</span><span class="p">,</span> <span class="n">min_samples</span><span class="o">=</span><span class="mi">5</span><span class="p">,</span> <span class="n">metric</span><span class="o">=</span><span class="s2">&quot;euclidean&quot;</span><span class="p">)</span>
<span class="n">dbscan_labels</span> <span class="o">=</span> <span class="n">dbscan</span><span class="o">.</span><span class="n">fit_predict</span><span class="p">(</span><span class="n">df_abstracts_pca</span><span class="p">)</span>
<span class="n">df_abstracts_dbscan</span> <span class="o">=</span> <span class="n">df_abstracts</span><span class="o">.</span><span class="n">copy</span><span class="p">()</span>
<span class="n">df_abstracts_dbscan</span><span class="p">[</span><span class="s2">&quot;cluster&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">dbscan_labels</span>
<span class="n">df_abstracts_dbscan</span><span class="p">[</span><span class="s2">&quot;cluster&quot;</span><span class="p">]</span><span class="o">.</span><span class="n">unique</span><span class="p">()</span>
<span class="n">df_abstracts_dbscan</span><span class="p">[</span><span class="n">df_abstracts_dbscan</span><span class="p">[</span><span class="s2">&quot;cluster&quot;</span><span class="p">]</span> <span class="o">==</span> <span class="mi">1</span><span class="p">][</span><span class="s2">&quot;title&quot;</span><span class="p">]</span>
</pre></div>

     </div>
</div>
</div>
</div>

<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>


<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt">Out[18]:</div>




<div class="jp-RenderedText jp-OutputArea-output jp-OutputArea-executeResult" data-mime-type="text/plain">
<pre>14     Imagining Buddhist modernism: the shared religious categories of scholars and American Buddhists
20              Why Durkheim really thought that Buddhism was a ‘religion’ (in memoriam Massimo Rosati)
158                                      Textbook Buddhism: introductory books on the Buddhist religion
439                                                                Recent trends in Sri Lankan Buddhism
471                                      William James and Buddhism: American Pragmatism and the Orient
559                     Buddhist Environmental Ethics and Detraditionalization: The Case of EcoBuddhism
620                                                                Buddhadharma and contemporary ethics
631                                                                   How environmentalist is Buddhism?
638                                                                                Protestant Buddhism?
690                Burial ‘ad sanctos’ and the physical presence of the Buddha in early Indian Buddhism
Name: title, dtype: object</pre>
</div>

</div>

</div>

</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell jp-mod-noOutputs  ">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&nbsp;[19]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
     <div class="CodeMirror cm-s-jupyter">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">pca</span> <span class="o">=</span> <span class="n">PCA</span><span class="p">(</span><span class="n">n_components</span><span class="o">=</span><span class="mi">2</span><span class="p">,</span> <span class="n">whiten</span><span class="o">=</span><span class="kc">False</span><span class="p">,</span> <span class="n">random_state</span><span class="o">=</span><span class="mi">42</span><span class="p">)</span>

<span class="n">dbscan_pca_2d</span> <span class="o">=</span> <span class="n">pca</span><span class="o">.</span><span class="n">fit_transform</span><span class="p">(</span><span class="n">df_abstracts_tfidf</span><span class="p">)</span>
<span class="n">df_dbscan_2d</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">DataFrame</span><span class="p">(</span><span class="n">data</span><span class="o">=</span><span class="n">dbscan_pca_2d</span><span class="p">,</span> <span class="n">columns</span><span class="o">=</span><span class="p">[</span><span class="s2">&quot;pc_1&quot;</span><span class="p">,</span> <span class="s2">&quot;pc_2&quot;</span><span class="p">])</span>
<span class="n">df_dbscan_2d</span><span class="p">[</span><span class="s2">&quot;clusters&quot;</span><span class="p">]</span> <span class="o">=</span> <span class="n">dbscan_labels</span>
</pre></div>

     </div>
</div>
</div>
</div>

</div><div class="jp-Cell jp-CodeCell jp-Notebook-cell   ">
<div class="jp-Cell-inputWrapper">
<div class="jp-Collapser jp-InputCollapser jp-Cell-inputCollapser">
</div>
<div class="jp-InputArea jp-Cell-inputArea">
<div class="jp-InputPrompt jp-InputArea-prompt">In&nbsp;[20]:</div>
<div class="jp-CodeMirrorEditor jp-Editor jp-InputArea-editor" data-type="inline">
     <div class="CodeMirror cm-s-jupyter">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">sns_plot</span> <span class="o">=</span> <span class="n">sns</span><span class="o">.</span><span class="n">scatterplot</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="s2">&quot;pc_1&quot;</span><span class="p">,</span> <span class="n">y</span><span class="o">=</span><span class="s2">&quot;pc_2&quot;</span><span class="p">,</span> <span class="n">hue</span><span class="o">=</span><span class="s2">&quot;clusters&quot;</span><span class="p">,</span> <span class="n">data</span><span class="o">=</span><span class="n">df_dbscan_2d</span><span class="p">)</span>
</pre></div>

     </div>
</div>
</div>
</div>

<div class="jp-Cell-outputWrapper">
<div class="jp-Collapser jp-OutputCollapser jp-Cell-outputCollapser">
</div>


<div class="jp-OutputArea jp-Cell-outputArea">

<div class="jp-OutputArea-child">

    
    <div class="jp-OutputPrompt jp-OutputArea-prompt"></div>




<div class="jp-RenderedImage jp-OutputArea-output ">
<img src="data:image/png;base64,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
"
class="
"
>
</div>

</div>

</div>

</div>

</div>
</body>







</html>
