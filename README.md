## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/Arthurhcf/sample_pages/edit/master/README.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Link do vídeo

// Read embed application token from textbox
var txtAccessToken = $('#txtAccessToken').val();

// Read embed URL from textbox
var txtEmbedUrl = $('#txtReportEmbed').val();

// Read report Id from textbox
var txtEmbedReportId = $('#txtEmbedReportId').val();

// Read embed type from radio
var tokenType = $('input:radio[name=tokenType]:checked').val();

// Get models. models contains enums that can be used.
var models = window['powerbi-client'].models;

// We give All permissions to demonstrate switching between View and Edit mode and saving report.
var permissions = models.Permissions.All;

// Embed configuration used to describe the what and how to embed.
// This object is used when calling powerbi.embed.
// This also includes settings and options such as filters.
// You can find more information at https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details.
var config = {
    type: 'report',
    tokenType: tokenType == '0' ? models.TokenType.Aad : models.TokenType.Embed,
    accessToken: txtAccessToken,
    embedUrl: txtEmbedUrl,
    id: txtEmbedReportId,
    permissions: permissions,
    settings: {
      panes: {
        filters: {
          visible: true
        },
        pageNavigation: {
          visible: true
        }
      }
    }
};

// Get a reference to the embedded report HTML element
var embedContainer = $('#embedContainer')[0];

// Embed the report and display it within the div container.
var report = powerbi.embed(embedContainer, config);

// Report.off removes a given event handler if it exists.
report.off("loaded");

// Report.on will add an event handler which prints to Log window.
report.on("loaded", function () {
    Log.logText("Loaded");
});

// Report.off removes a given event handler if it exists.
report.off("rendered");

// Report.on will add an event handler which prints to Log window.
report.on("rendered", function () {
    Log.logText("Rendered");
});

report.on("error", function (event) {
    Log.log(event.detail);

    report.off("error");
});

report.off("saved");
report.on("saved", function (event) {
    Log.log(event.detail);
    if (event.detail.saveAs) {
        Log.logText('In order to interact with the new report, create a new token and load the new report');
    }
});

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/Arthurhcf/sample_pages/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
