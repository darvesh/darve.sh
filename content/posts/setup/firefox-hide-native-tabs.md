---
title: "Hide Native Tabs in Firefox"
description: "Hide native Firefox tabs using custom CSS"
date: "2022-05-24"
tags: ["Firefox"]
categories: ["browser"]
aliases: ["hide-native-tabs-firefox"]
ShowToc: false
TocOpen: true
---

1. Visit `about:config`
2. Search and enable `toolkit.legacyUserProfileCustomizations.stylesheets`
3. Visit `about:support`
4. Click on `Open Directory` which is to the right of `Profile Directory`
5. Create a new folder called `chrome`
6. Open chrome and create a new file named `userChome.css`
7. Paste the following
```css
#tabbrowser-tabs {
  visibility: collapse;
}

#titlebar #TabsToolbar {
  background-color: var(--toolbar-bgcolor);
  background-image: var(--toolbar-bgimage);
  padding-top: 5px;
}
```

Tested on Firefox v100.0.2.