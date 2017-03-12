## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/howeecross/device_samsung_n7000/edit/master/index.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

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

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/howeecross/device_samsung_n7000/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or """
Legacy module - don't use in new code!

html5lib now has its own proper implementation.

This module implements a tree builder for html5lib that generates lxml
html element trees.  This module uses camelCase as it follows the
html5lib style guide.
"""

from html5lib.treebuilders import _base, etree as etree_builders
from lxml import html, etree


class DocumentType(object):

    def __init__(self, name, publicId, systemId):
        self.name = name
        self.publicId = publicId
        self.systemId = systemId

class Document(object):

    def __init__(self):
        self._elementTree = None
        self.childNodes = []

    def appendChild(self, element):
        self._elementTree.getroot().addnext(element._element)


class TreeBuilder(_base.TreeBuilder):
    documentClass = Document
    doctypeClass = DocumentType
    elementClass = None
    commentClass = None
    fragmentClass = Document

    def __init__(self, *args, **kwargs):
        html_builder = etree_builders.getETreeModule(html, fullTree=False)
        etree_builder = etree_builders.getETreeModule(etree, fullTree=False)
        self.elementClass = html_builder.Element
        self.commentClass = etree_builder.Comment
        _base.TreeBuilder.__init__(self, *args, **kwargs)

    def reset(self):
        _base.TreeBuilder.reset(self)
        self.rootInserted = False
        self.initialComments = []
        self.doctype = None

    def getDocument(self):
        return self.document._elementTree

    def getFragment(self):
        fragment = []
        element = self.openElements[0]._element
        if element.text:
            fragment.append(element.text)
        fragment.extend(element.getchildren())
        if element.tail:
            fragment.append(element.tail)
        return fragment

    def insertDoctype(self, name, publicId, systemId):
        doctype = self.doctypeClass(name, publicId, systemId)
        self.doctype = doctype

    def insertComment(self, data, parent=None):
        if not self.rootInserted:
            self.initialComments.append(data)
        else:
            _base.TreeBuilder.insertComment(self, data, parent)

    def insertRoot(self, name):
        buf = []
        if self.doctype and self.doctype.name:
            buf.append('<!DOCTYPE %s' % self.doctype.name)
            if self.doctype.publicId is not None or self.doctype.systemId is not None:
                buf.append(' PUBLIC "%s" "%s"' % (self.doctype.publicId,
                                                  self.doctype.systemId))
            buf.append('>')
        buf.append('<html></html>')
        root = html.fromstring(''.join(buf))

        # Append the initial comments:
        for comment in self.initialComments:
            root.addprevious(etree.Comment(comment))

        # Create the root document and add the ElementTree to it
        self.document = self.documentClass()
        self.document._elementTree = root.getroottree()

        # Add the root element to the internal child/open data structures
        root_element = self.elementClass(name)
        root_element._element = root
        self.document.childNodes.append(root_element)
        self.openElements.append(root_element)

        self.rootInserted = True
[contact support](https://github.com/contact) and we’ll help you sort it out.
