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
This XML file does not appear to have any style information associated with it. The document tree is shown below.
<root>
<version value="131091"/>
<min_engine_version value="0x0003000a"/>
<GPU_Serial_List count="7">
<serial name="Adreno">
<default_value>
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="0"/>
<MPEG4_FWVGA_DEC count="2"/>
<H264_FWVGA_DEC count="2"/>
<H264_FWVGA_INTERLACE_DEC count="0"/>
<MPEG4_720P_DEC count="2"/>
<H264_720P_DEC count="2"/>
<H264_720P_INTERLACE_DEC count="0"/>
<MPEG4_1080P_DEC count="2"/>
<H264_1080P_DEC count="2"/>
<H264_1080P_INTERLACE_DEC count="0"/>
<H264_2K_DEC count="0"/>
<H264_2K_INTERLACE_DEC count="0"/>
<H264_4K_DEC count="0"/>
<H264_4K_INTERLACE_DEC count="0"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="1"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="1"/>
<!--
IMPORT_FORMAT 
    		  typedef enum
					{
					    MV2_1080P_MPEG4,  // 0
						MV2_720P_MPEG4,   // 1
						MV2_FWVGA_MPEG4,  // 2
						MV2_VGA_MPEG4,    // 3
						MV2_4K_H264,      // 4
						MV2_1080P_H264,   // 5
						MV2_720P_H264,    // 6
						MV2_FWVGA_H264,   // 7
						MV2_VGA_H264,     // 8
						MV2_4K_H264_INTERLACE, // 9
						MV2_1080P_H264_INTERLACE, // 10
						MV2_720P_H264_INTERLACE,  // 11
						MV2_FWVGA_H264_INTERLACE, // 12
						MV2_VGA_H264_INTERLACE    // 13
					}MV2_HW_DEC_RESOLUTION;
 						
-->
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="8" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="6" hw_enc="6" pip="3" reverse="6"/>
<BETA_TESTED_FLAG value="0"/>
</default_value>
<GPU_List count="15">
<GPU name="Adreno (TM) 1">
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="0"/>
<MPEG4_FWVGA_DEC count="1"/>
<H264_FWVGA_DEC count="1"/>
<H264_FWVGA_INTERLACE_DEC count="0"/>
<MPEG4_720P_DEC count="1"/>
<H264_720P_DEC count="1"/>
<H264_720P_INTERLACE_DEC count="0"/>
<MPEG4_1080P_DEC count="1"/>
<H264_1080P_DEC count="1"/>
<H264_1080P_INTERLACE_DEC count="0"/>
<H264_2K_DEC count="0"/>
<H264_2K_INTERLACE_DEC count="0"/>
<H264_4K_DEC count="0"/>
<H264_4K_INTERLACE_DEC count="0"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="0"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="0"/>
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="3" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="3" hw_enc="3" pip="3" reverse="3"/>
<BETA_TESTED_FLAG value="0"/>
</GPU>
<GPU name="Adreno (TM) 2">
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="0"/>
<MPEG4_FWVGA_DEC count="1"/>
<H264_FWVGA_DEC count="1"/>
<H264_FWVGA_INTERLACE_DEC count="0"/>
<MPEG4_720P_DEC count="1"/>
<H264_720P_DEC count="1"/>
<H264_720P_INTERLACE_DEC count="0"/>
<MPEG4_1080P_DEC count="1"/>
<H264_1080P_DEC count="1"/>
<H264_1080P_INTERLACE_DEC count="0"/>
<H264_2K_DEC count="0"/>
<H264_2K_INTERLACE_DEC count="0"/>
<H264_4K_DEC count="0"/>
<H264_4K_INTERLACE_DEC count="0"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="0"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="0"/>
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="3" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="3" hw_enc="3" pip="3" reverse="3"/>
<BETA_TESTED_FLAG value="0"/>
</GPU>
<GPU name="Adreno (TM) 304">
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="0"/>
<MPEG4_FWVGA_DEC count="2"/>
<H264_FWVGA_DEC count="2"/>
<H264_FWVGA_INTERLACE_DEC count="0"/>
<MPEG4_720P_DEC count="1"/>
<H264_720P_DEC count="1"/>
<H264_720P_INTERLACE_DEC count="0"/>
<MPEG4_1080P_DEC count="0"/>
<H264_1080P_DEC count="0"/>
<H264_1080P_INTERLACE_DEC count="0"/>
<H264_2K_DEC count="0"/>
<H264_2K_INTERLACE_DEC count="0"/>
<H264_4K_DEC count="0"/>
<H264_4K_INTERLACE_DEC count="0"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="1"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="1"/>
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="3" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="3" hw_enc="3" pip="3" reverse="3"/>
<BETA_TESTED_FLAG value="0"/>
</GPU>
<GPU name="Adreno (TM) 305">
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="0"/>
<MPEG4_FWVGA_DEC count="2"/>
<H264_FWVGA_DEC count="2"/>
<H264_FWVGA_INTERLACE_DEC count="0"/>
<MPEG4_720P_DEC count="1"/>
<H264_720P_DEC count="1"/>
<H264_720P_INTERLACE_DEC count="0"/>
<MPEG4_1080P_DEC count="0"/>
<H264_1080P_DEC count="0"/>
<H264_1080P_INTERLACE_DEC count="0"/>
<H264_2K_DEC count="0"/>
<H264_2K_INTERLACE_DEC count="0"/>
<H264_4K_DEC count="0"/>
<H264_4K_INTERLACE_DEC count="0"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="1"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="1"/>
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="3" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="6" hw_enc="6" pip="3" reverse="6"/>
<BETA_TESTED_FLAG value="0"/>
</GPU>
<GPU name="Adreno (TM) 306">
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="0"/>
<MPEG4_FWVGA_DEC count="2"/>
<H264_FWVGA_DEC count="2"/>
<H264_FWVGA_INTERLACE_DEC count="0"/>
<MPEG4_720P_DEC count="1"/>
<H264_720P_DEC count="1"/>
<H264_720P_INTERLACE_DEC count="0"/>
<MPEG4_1080P_DEC count="1"/>
<H264_1080P_DEC count="1"/>
<H264_1080P_INTERLACE_DEC count="0"/>
<H264_2K_DEC count="0"/>
<H264_2K_INTERLACE_DEC count="0"/>
<H264_4K_DEC count="0"/>
<H264_4K_INTERLACE_DEC count="0"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="1"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="1"/>
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="8" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="6" hw_enc="6" pip="3" reverse="6"/>
<BETA_TESTED_FLAG value="0"/>
</GPU>
<GPU name="Adreno (TM) 320">
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="0"/>
<MPEG4_FWVGA_DEC count="2"/>
<H264_FWVGA_DEC count="2"/>
<H264_FWVGA_INTERLACE_DEC count="0"/>
<MPEG4_720P_DEC count="2"/>
<H264_720P_DEC count="2"/>
<H264_720P_INTERLACE_DEC count="0"/>
<MPEG4_1080P_DEC count="2"/>
<H264_1080P_DEC count="2"/>
<H264_1080P_INTERLACE_DEC count="0"/>
<H264_2K_DEC count="0"/>
<H264_2K_INTERLACE_DEC count="0"/>
<H264_4K_DEC count="0"/>
<H264_4K_INTERLACE_DEC count="0"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="1"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="1"/>
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="8" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="6" hw_enc="6" pip="3" reverse="6"/>
<BETA_TESTED_FLAG value="1"/>
</GPU>
<GPU name="Adreno (TM) 330">
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="0"/>
<MPEG4_FWVGA_DEC count="5"/>
<H264_FWVGA_DEC count="5"/>
<H264_FWVGA_INTERLACE_DEC count="0"/>
<MPEG4_720P_DEC count="5"/>
<H264_720P_DEC count="5"/>
<H264_720P_INTERLACE_DEC count="0"/>
<MPEG4_1080P_DEC count="5"/>
<H264_1080P_DEC count="5"/>
<H264_1080P_INTERLACE_DEC count="0"/>
<H264_2K_DEC count="1"/>
<H264_2K_INTERLACE_DEC count="0"/>
<H264_4K_DEC count="1"/>
<H264_4K_INTERLACE_DEC count="0"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="1"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="1"/>
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="8" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="6" hw_enc="5" pip="3" reverse="6"/>
<BETA_TESTED_FLAG value="1"/>
</GPU>
<GPU name="Adreno (TM) 405">
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="0"/>
<MPEG4_FWVGA_DEC count="2"/>
<H264_FWVGA_DEC count="2"/>
<H264_FWVGA_INTERLACE_DEC count="0"/>
<MPEG4_720P_DEC count="2"/>
<H264_720P_DEC count="2"/>
<H264_720P_INTERLACE_DEC count="0"/>
<MPEG4_1080P_DEC count="1"/>
<H264_1080P_DEC count="1"/>
<H264_1080P_INTERLACE_DEC count="0"/>
<H264_2K_DEC count="0"/>
<H264_2K_INTERLACE_DEC count="0"/>
<H264_4K_DEC count="0"/>
<H264_4K_INTERLACE_DEC count="0"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="1"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="1"/>
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="8" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="6" hw_enc="6" pip="3" reverse="6"/>
<BETA_TESTED_FLAG value="0"/>
</GPU>
<GPU name="Adreno (TM) 418">
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="0"/>
<MPEG4_FWVGA_DEC count="2"/>
<H264_FWVGA_DEC count="2"/>
<H264_FWVGA_INTERLACE_DEC count="0"/>
<MPEG4_720P_DEC count="2"/>
<H264_720P_DEC count="2"/>
<H264_720P_INTERLACE_DEC count="0"/>
<MPEG4_1080P_DEC count="2"/>
<H264_1080P_DEC count="2"/>
<H264_1080P_INTERLACE_DEC count="0"/>
<H264_2K_DEC count="0"/>
<H264_2K_INTERLACE_DEC count="0"/>
<H264_4K_DEC count="0"/>
<H264_4K_INTERLACE_DEC count="0"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="1"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="1"/>
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="8" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="6" hw_enc="6" pip="3" reverse="6"/>
<BETA_TESTED_FLAG value="1"/>
</GPU>
<GPU name="Adreno (TM) 420">
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="0"/>
<MPEG4_FWVGA_DEC count="5"/>
<H264_FWVGA_DEC count="5"/>
<H264_FWVGA_INTERLACE_DEC count="0"/>
<MPEG4_720P_DEC count="5"/>
<H264_720P_DEC count="5"/>
<H264_720P_INTERLACE_DEC count="0"/>
<MPEG4_1080P_DEC count="5"/>
<H264_1080P_DEC count="5"/>
<H264_1080P_INTERLACE_DEC count="0"/>
<H264_2K_DEC count="1"/>
<H264_2K_INTERLACE_DEC count="0"/>
<H264_4K_DEC count="1"/>
<H264_4K_INTERLACE_DEC count="0"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="1"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="1"/>
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="8" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="6" hw_enc="5" pip="3" reverse="6"/>
<BETA_TESTED_FLAG value="1"/>
</GPU>
<GPU name="Adreno (TM) 430">
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="0"/>
<MPEG4_FWVGA_DEC count="5"/>
<H264_FWVGA_DEC count="5"/>
<H264_FWVGA_INTERLACE_DEC count="0"/>
<MPEG4_720P_DEC count="5"/>
<H264_720P_DEC count="5"/>
<H264_720P_INTERLACE_DEC count="0"/>
<MPEG4_1080P_DEC count="5"/>
<H264_1080P_DEC count="5"/>
<H264_1080P_INTERLACE_DEC count="0"/>
<H264_2K_DEC count="1"/>
<H264_2K_INTERLACE_DEC count="0"/>
<H264_4K_DEC count="1"/>
<H264_4K_INTERLACE_DEC count="0"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="1"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="1"/>
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="8" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="6" hw_enc="5" pip="3" reverse="6"/>
<BETA_TESTED_FLAG value="1"/>
</GPU>
<GPU name="Adreno (TM) 505">
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="0"/>
<MPEG4_FWVGA_DEC count="4"/>
<H264_FWVGA_DEC count="4"/>
<H264_FWVGA_INTERLACE_DEC count="0"/>
<MPEG4_720P_DEC count="2"/>
<H264_720P_DEC count="2"/>
<H264_720P_INTERLACE_DEC count="0"/>
<MPEG4_1080P_DEC count="2"/>
<H264_1080P_DEC count="2"/>
<H264_1080P_INTERLACE_DEC count="0"/>
<H264_2K_DEC count="0"/>
<H264_2K_INTERLACE_DEC count="0"/>
<H264_4K_DEC count="0"/>
<H264_4K_INTERLACE_DEC count="0"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="1"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="1"/>
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="8" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="6" hw_enc="6" pip="3" reverse="6"/>
<BETA_TESTED_FLAG value="1"/>
</GPU>
<GPU name="Adreno (TM) 506">
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="0"/>
<MPEG4_FWVGA_DEC count="4"/>
<H264_FWVGA_DEC count="4"/>
<H264_FWVGA_INTERLACE_DEC count="0"/>
<MPEG4_720P_DEC count="2"/>
<H264_720P_DEC count="2"/>
<H264_720P_INTERLACE_DEC count="0"/>
<MPEG4_1080P_DEC count="2"/>
<H264_1080P_DEC count="2"/>
<H264_1080P_INTERLACE_DEC count="0"/>
<H264_2K_DEC count="0"/>
<H264_2K_INTERLACE_DEC count="0"/>
<H264_4K_DEC count="0"/>
<H264_4K_INTERLACE_DEC count="0"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="1"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="1"/>
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="8" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="6" hw_enc="6" pip="3" reverse="6"/>
<BETA_TESTED_FLAG value="1"/>
</GPU>
<GPU name="Adreno (TM) 510">
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="0"/>
<MPEG4_FWVGA_DEC count="4"/>
<H264_FWVGA_DEC count="4"/>
<H264_FWVGA_INTERLACE_DEC count="0"/>
<MPEG4_720P_DEC count="2"/>
<H264_720P_DEC count="2"/>
<H264_720P_INTERLACE_DEC count="0"/>
<MPEG4_1080P_DEC count="2"/>
<H264_1080P_DEC count="2"/>
<H264_1080P_INTERLACE_DEC count="0"/>
<H264_2K_DEC count="0"/>
<H264_2K_INTERLACE_DEC count="0"/>
<H264_4K_DEC count="0"/>
<H264_4K_INTERLACE_DEC count="0"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="1"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="1"/>
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="8" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="6" hw_enc="6" pip="3" reverse="6"/>
<BETA_TESTED_FLAG value="1"/>
</GPU>
<GPU name="Adreno (TM) 530">
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="0"/>
<MPEG4_FWVGA_DEC count="5"/>
<H264_FWVGA_DEC count="5"/>
<H264_FWVGA_INTERLACE_DEC count="0"/>
<MPEG4_720P_DEC count="5"/>
<H264_720P_DEC count="5"/>
<H264_720P_INTERLACE_DEC count="0"/>
<MPEG4_1080P_DEC count="5"/>
<H264_1080P_DEC count="5"/>
<H264_1080P_INTERLACE_DEC count="0"/>
<H264_2K_DEC count="1"/>
<H264_2K_INTERLACE_DEC count="0"/>
<H264_4K_DEC count="1"/>
<H264_4K_INTERLACE_DEC count="0"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="1"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="1"/>
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="8" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="6" hw_enc="5" pip="3" reverse="6"/>
<BETA_TESTED_FLAG value="1"/>
</GPU>
</GPU_List>
</serial>
<serial name="Mali">
<default_value>
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="-1"/>
<MPEG4_FWVGA_DEC count="2"/>
<H264_FWVGA_DEC count="2"/>
<H264_FWVGA_INTERLACE_DEC count="2"/>
<MPEG4_720P_DEC count="2"/>
<H264_720P_DEC count="2"/>
<H264_720P_INTERLACE_DEC count="2"/>
<MPEG4_1080P_DEC count="2"/>
<H264_1080P_DEC count="2"/>
<H264_1080P_INTERLACE_DEC count="2"/>
<H264_2K_DEC count="0"/>
<H264_2K_INTERLACE_DEC count="0"/>
<H264_4K_DEC count="0"/>
<H264_4K_INTERLACE_DEC count="0"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="1"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="1"/>
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="8" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="6" hw_enc="6" pip="3" reverse="6"/>
<BETA_TESTED_FLAG value="0"/>
</default_value>
<GPU_List count="22">
<GPU name="Mali-2">
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="-1"/>
<MPEG4_FWVGA_DEC count="1"/>
<H264_FWVGA_DEC count="1"/>
<H264_FWVGA_INTERLACE_DEC count="1"/>
<MPEG4_720P_DEC count="1"/>
<H264_720P_DEC count="1"/>
<H264_720P_INTERLACE_DEC count="1"/>
<MPEG4_1080P_DEC count="1"/>
<H264_1080P_DEC count="1"/>
<H264_1080P_INTERLACE_DEC count="1"/>
<H264_2K_DEC count="0"/>
<H264_2K_INTERLACE_DEC count="0"/>
<H264_4K_DEC count="0"/>
<H264_4K_INTERLACE_DEC count="0"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="0"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="0"/>
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="3" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="3" hw_enc="3" pip="3" reverse="3"/>
<BETA_TESTED_FLAG value="0"/>
</GPU>
<GPU name="Mali-3">
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="-1"/>
<MPEG4_FWVGA_DEC count="1"/>
<H264_FWVGA_DEC count="1"/>
<H264_FWVGA_INTERLACE_DEC count="1"/>
<MPEG4_720P_DEC count="1"/>
<H264_720P_DEC count="1"/>
<H264_720P_INTERLACE_DEC count="1"/>
<MPEG4_1080P_DEC count="1"/>
<H264_1080P_DEC count="1"/>
<H264_1080P_INTERLACE_DEC count="1"/>
<H264_2K_DEC count="0"/>
<H264_2K_INTERLACE_DEC count="0"/>
<H264_4K_DEC count="0"/>
<H264_4K_INTERLACE_DEC count="0"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="0"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="0"/>
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="3" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="3" hw_enc="3" pip="3" reverse="3"/>
<BETA_TESTED_FLAG value="0"/>
</GPU>
<GPU name="Mali-400 MP">
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="-1"/>
<MPEG4_FWVGA_DEC count="2"/>
<H264_FWVGA_DEC count="2"/>
<H264_FWVGA_INTERLACE_DEC count="2"/>
<MPEG4_720P_DEC count="2"/>
<H264_720P_DEC count="2"/>
<H264_720P_INTERLACE_DEC count="2"/>
<MPEG4_1080P_DEC count="1"/>
<H264_1080P_DEC count="1"/>
<H264_1080P_INTERLACE_DEC count="1"/>
<H264_2K_DEC count="0"/>
<H264_2K_INTERLACE_DEC count="0"/>
<H264_4K_DEC count="0"/>
<H264_4K_INTERLACE_DEC count="0"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="1"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="1"/>
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="8" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="6" hw_enc="6" pip="3" reverse="6"/>
<BETA_TESTED_FLAG value="0"/>
</GPU>
<GPU name="Mali-450 MP">
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="-1"/>
<MPEG4_FWVGA_DEC count="4"/>
<H264_FWVGA_DEC count="4"/>
<H264_FWVGA_INTERLACE_DEC count="4"/>
<MPEG4_720P_DEC count="2"/>
<H264_720P_DEC count="2"/>
<H264_720P_INTERLACE_DEC count="2"/>
<MPEG4_1080P_DEC count="2"/>
<H264_1080P_DEC count="2"/>
<H264_1080P_INTERLACE_DEC count="2"/>
<H264_2K_DEC count="0"/>
<H264_2K_INTERLACE_DEC count="0"/>
<H264_4K_DEC count="0"/>
<H264_4K_INTERLACE_DEC count="0"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="1"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="1"/>
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="8" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="6" hw_enc="6" pip="3" reverse="6"/>
<BETA_TESTED_FLAG value="1"/>
</GPU>
<GPU name="Mali-T622">
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="-1"/>
<MPEG4_FWVGA_DEC count="3"/>
<H264_FWVGA_DEC count="3"/>
<H264_FWVGA_INTERLACE_DEC count="3"/>
<MPEG4_720P_DEC count="3"/>
<H264_720P_DEC count="3"/>
<H264_720P_INTERLACE_DEC count="3"/>
<MPEG4_1080P_DEC count="3"/>
<H264_1080P_DEC count="3"/>
<H264_1080P_INTERLACE_DEC count="3"/>
<H264_2K_DEC count="1"/>
<H264_2K_INTERLACE_DEC count="1"/>
<H264_4K_DEC count="0"/>
<H264_4K_INTERLACE_DEC count="0"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="1"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="1"/>
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="8" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="6" hw_enc="5" pip="3" reverse="6"/>
<BETA_TESTED_FLAG value="1"/>
</GPU>
<GPU name="Mali-T624">
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="-1"/>
<MPEG4_FWVGA_DEC count="3"/>
<H264_FWVGA_DEC count="3"/>
<H264_FWVGA_INTERLACE_DEC count="3"/>
<MPEG4_720P_DEC count="3"/>
<H264_720P_DEC count="3"/>
<H264_720P_INTERLACE_DEC count="3"/>
<MPEG4_1080P_DEC count="3"/>
<H264_1080P_DEC count="3"/>
<H264_1080P_INTERLACE_DEC count="3"/>
<H264_2K_DEC count="1"/>
<H264_2K_INTERLACE_DEC count="1"/>
<H264_4K_DEC count="0"/>
<H264_4K_INTERLACE_DEC count="0"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="1"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="1"/>
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="8" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="6" hw_enc="5" pip="3" reverse="6"/>
<BETA_TESTED_FLAG value="1"/>
</GPU>
<GPU name="Mali-T628">
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="-1"/>
<MPEG4_FWVGA_DEC count="3"/>
<H264_FWVGA_DEC count="3"/>
<H264_FWVGA_INTERLACE_DEC count="3"/>
<MPEG4_720P_DEC count="3"/>
<H264_720P_DEC count="3"/>
<H264_720P_INTERLACE_DEC count="3"/>
<MPEG4_1080P_DEC count="3"/>
<H264_1080P_DEC count="3"/>
<H264_1080P_INTERLACE_DEC count="3"/>
<H264_2K_DEC count="1"/>
<H264_2K_INTERLACE_DEC count="1"/>
<H264_4K_DEC count="0"/>
<H264_4K_INTERLACE_DEC count="0"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="1"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="1"/>
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="8" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="6" hw_enc="5" pip="3" reverse="6"/>
<BETA_TESTED_FLAG value="1"/>
</GPU>
<GPU name="Mali-T62">
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="-1"/>
<MPEG4_FWVGA_DEC count="3"/>
<H264_FWVGA_DEC count="3"/>
<H264_FWVGA_INTERLACE_DEC count="3"/>
<MPEG4_720P_DEC count="3"/>
<H264_720P_DEC count="3"/>
<H264_720P_INTERLACE_DEC count="3"/>
<MPEG4_1080P_DEC count="3"/>
<H264_1080P_DEC count="3"/>
<H264_1080P_INTERLACE_DEC count="3"/>
<H264_2K_DEC count="1"/>
<H264_2K_INTERLACE_DEC count="1"/>
<H264_4K_DEC count="0"/>
<H264_4K_INTERLACE_DEC count="0"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="1"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="1"/>
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="8" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="6" hw_enc="5" pip="3" reverse="6"/>
<BETA_TESTED_FLAG value="0"/>
</GPU>
<GPU name="Mali-T720">
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="-1"/>
<MPEG4_FWVGA_DEC count="3"/>
<H264_FWVGA_DEC count="3"/>
<H264_FWVGA_INTERLACE_DEC count="3"/>
<MPEG4_720P_DEC count="3"/>
<H264_720P_DEC count="3"/>
<H264_720P_INTERLACE_DEC count="3"/>
<MPEG4_1080P_DEC count="3"/>
<H264_1080P_DEC count="3"/>
<H264_1080P_INTERLACE_DEC count="3"/>
<H264_2K_DEC count="1"/>
<H264_2K_INTERLACE_DEC count="1"/>
<H264_4K_DEC count="0"/>
<H264_4K_INTERLACE_DEC count="0"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="1"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="1"/>
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="8" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="6" hw_enc="5" pip="3" reverse="6"/>
<BETA_TESTED_FLAG value="1"/>
</GPU>
<GPU name="Mali-T72">
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="-1"/>
<MPEG4_FWVGA_DEC count="3"/>
<H264_FWVGA_DEC count="3"/>
<H264_FWVGA_INTERLACE_DEC count="3"/>
<MPEG4_720P_DEC count="3"/>
<H264_720P_DEC count="3"/>
<H264_720P_INTERLACE_DEC count="3"/>
<MPEG4_1080P_DEC count="3"/>
<H264_1080P_DEC count="3"/>
<H264_1080P_INTERLACE_DEC count="3"/>
<H264_2K_DEC count="1"/>
<H264_2K_INTERLACE_DEC count="1"/>
<H264_4K_DEC count="0"/>
<H264_4K_INTERLACE_DEC count="0"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="1"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="1"/>
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="8" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="6" hw_enc="5" pip="3" reverse="6"/>
<BETA_TESTED_FLAG value="0"/>
</GPU>
<GPU name="Mali-T760">
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="-1"/>
<MPEG4_FWVGA_DEC count="5"/>
<H264_FWVGA_DEC count="5"/>
<H264_FWVGA_INTERLACE_DEC count="5"/>
<MPEG4_720P_DEC count="5"/>
<H264_720P_DEC count="5"/>
<H264_720P_INTERLACE_DEC count="5"/>
<MPEG4_1080P_DEC count="5"/>
<H264_1080P_DEC count="5"/>
<H264_1080P_INTERLACE_DEC count="5"/>
<H264_2K_DEC count="1"/>
<H264_2K_INTERLACE_DEC count="1"/>
<H264_4K_DEC count="1"/>
<H264_4K_INTERLACE_DEC count="1"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="1"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="1"/>
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="8" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="6" hw_enc="5" pip="3" reverse="6"/>
<BETA_TESTED_FLAG value="1"/>
</GPU>
<GPU name="Mali-T764">
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="-1"/>
<MPEG4_FWVGA_DEC count="5"/>
<H264_FWVGA_DEC count="5"/>
<H264_FWVGA_INTERLACE_DEC count="5"/>
<MPEG4_720P_DEC count="5"/>
<H264_720P_DEC count="5"/>
<H264_720P_INTERLACE_DEC count="5"/>
<MPEG4_1080P_DEC count="5"/>
<H264_1080P_DEC count="5"/>
<H264_1080P_INTERLACE_DEC count="5"/>
<H264_2K_DEC count="1"/>
<H264_2K_INTERLACE_DEC count="1"/>
<H264_4K_DEC count="1"/>
<H264_4K_INTERLACE_DEC count="1"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="1"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="1"/>
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="8" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="6" hw_enc="5" pip="3" reverse="6"/>
<BETA_TESTED_FLAG value="1"/>
</GPU>
<GPU name="Mali-T76">
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="-1"/>
<MPEG4_FWVGA_DEC count="5"/>
<H264_FWVGA_DEC count="5"/>
<H264_FWVGA_INTERLACE_DEC count="5"/>
<MPEG4_720P_DEC count="5"/>
<H264_720P_DEC count="5"/>
<H264_720P_INTERLACE_DEC count="5"/>
<MPEG4_1080P_DEC count="5"/>
<H264_1080P_DEC count="5"/>
<H264_1080P_INTERLACE_DEC count="5"/>
<H264_2K_DEC count="1"/>
<H264_2K_INTERLACE_DEC count="1"/>
<H264_4K_DEC count="1"/>
<H264_4K_INTERLACE_DEC count="1"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="1"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="1"/>
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="8" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="6" hw_enc="5" pip="3" reverse="6"/>
<BETA_TESTED_FLAG value="0"/>
</GPU>
<GPU name="Mali-T820">
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="-1"/>
<MPEG4_FWVGA_DEC count="3"/>
<H264_FWVGA_DEC count="3"/>
<H264_FWVGA_INTERLACE_DEC count="3"/>
<MPEG4_720P_DEC count="3"/>
<H264_720P_DEC count="3"/>
<H264_720P_INTERLACE_DEC count="3"/>
<MPEG4_1080P_DEC count="3"/>
<H264_1080P_DEC count="3"/>
<H264_1080P_INTERLACE_DEC count="3"/>
<H264_2K_DEC count="1"/>
<H264_2K_INTERLACE_DEC count="1"/>
<H264_4K_DEC count="0"/>
<H264_4K_INTERLACE_DEC count="0"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="1"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="1"/>
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="8" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="6" hw_enc="5" pip="3" reverse="6"/>
<BETA_TESTED_FLAG value="1"/>
</GPU>
<GPU name="Mali-T82">
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="-1"/>
<MPEG4_FWVGA_DEC count="3"/>
<H264_FWVGA_DEC count="3"/>
<H264_FWVGA_INTERLACE_DEC count="3"/>
<MPEG4_720P_DEC count="3"/>
<H264_720P_DEC count="3"/>
<H264_720P_INTERLACE_DEC count="3"/>
<MPEG4_1080P_DEC count="3"/>
<H264_1080P_DEC count="3"/>
<H264_1080P_INTERLACE_DEC count="3"/>
<H264_2K_DEC count="1"/>
<H264_2K_INTERLACE_DEC count="1"/>
<H264_4K_DEC count="0"/>
<H264_4K_INTERLACE_DEC count="0"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="1"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="1"/>
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="8" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="6" hw_enc="5" pip="3" reverse="6"/>
<BETA_TESTED_FLAG value="0"/>
</GPU>
<GPU name="Mali-T830">
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="-1"/>
<MPEG4_FWVGA_DEC count="3"/>
<H264_FWVGA_DEC count="3"/>
<H264_FWVGA_INTERLACE_DEC count="3"/>
<MPEG4_720P_DEC count="3"/>
<H264_720P_DEC count="3"/>
<H264_720P_INTERLACE_DEC count="3"/>
<MPEG4_1080P_DEC count="3"/>
<H264_1080P_DEC count="3"/>
<H264_1080P_INTERLACE_DEC count="3"/>
<H264_2K_DEC count="1"/>
<H264_2K_INTERLACE_DEC count="1"/>
<H264_4K_DEC count="0"/>
<H264_4K_INTERLACE_DEC count="0"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="1"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="1"/>
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="8" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="6" hw_enc="5" pip="3" reverse="6"/>
<BETA_TESTED_FLAG value="1"/>
</GPU>
<GPU name="Mali-T83">
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="-1"/>
<MPEG4_FWVGA_DEC count="3"/>
<H264_FWVGA_DEC count="3"/>
<H264_FWVGA_INTERLACE_DEC count="3"/>
<MPEG4_720P_DEC count="3"/>
<H264_720P_DEC count="3"/>
<H264_720P_INTERLACE_DEC count="3"/>
<MPEG4_1080P_DEC count="3"/>
<H264_1080P_DEC count="3"/>
<H264_1080P_INTERLACE_DEC count="3"/>
<H264_2K_DEC count="1"/>
<H264_2K_INTERLACE_DEC count="1"/>
<H264_4K_DEC count="0"/>
<H264_4K_INTERLACE_DEC count="0"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="1"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="1"/>
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="8" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="6" hw_enc="5" pip="3" reverse="6"/>
<BETA_TESTED_FLAG value="0"/>
</GPU>
<GPU name="Mali-T860">
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="-1"/>
<MPEG4_FWVGA_DEC count="5"/>
<H264_FWVGA_DEC count="5"/>
<H264_FWVGA_INTERLACE_DEC count="5"/>
<MPEG4_720P_DEC count="5"/>
<H264_720P_DEC count="5"/>
<H264_720P_INTERLACE_DEC count="5"/>
<MPEG4_1080P_DEC count="5"/>
<H264_1080P_DEC count="5"/>
<H264_1080P_INTERLACE_DEC count="5"/>
<H264_2K_DEC count="1"/>
<H264_2K_INTERLACE_DEC count="1"/>
<H264_4K_DEC count="1"/>
<H264_4K_INTERLACE_DEC count="1"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="1"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="1"/>
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="8" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="6" hw_enc="5" pip="3" reverse="6"/>
<BETA_TESTED_FLAG value="1"/>
</GPU>
<GPU name="Mali-T86">
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="-1"/>
<MPEG4_FWVGA_DEC count="5"/>
<H264_FWVGA_DEC count="5"/>
<H264_FWVGA_INTERLACE_DEC count="5"/>
<MPEG4_720P_DEC count="5"/>
<H264_720P_DEC count="5"/>
<H264_720P_INTERLACE_DEC count="5"/>
<MPEG4_1080P_DEC count="5"/>
<H264_1080P_DEC count="5"/>
<H264_1080P_INTERLACE_DEC count="5"/>
<H264_2K_DEC count="1"/>
<H264_2K_INTERLACE_DEC count="1"/>
<H264_4K_DEC count="1"/>
<H264_4K_INTERLACE_DEC count="1"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="1"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="1"/>
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="8" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="6" hw_enc="5" pip="3" reverse="6"/>
<BETA_TESTED_FLAG value="0"/>
</GPU>
<GPU name="Mali-T880">
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="-1"/>
<MPEG4_FWVGA_DEC count="5"/>
<H264_FWVGA_DEC count="5"/>
<H264_FWVGA_INTERLACE_DEC count="5"/>
<MPEG4_720P_DEC count="5"/>
<H264_720P_DEC count="5"/>
<H264_720P_INTERLACE_DEC count="5"/>
<MPEG4_1080P_DEC count="5"/>
<H264_1080P_DEC count="5"/>
<H264_1080P_INTERLACE_DEC count="5"/>
<H264_2K_DEC count="1"/>
<H264_2K_INTERLACE_DEC count="1"/>
<H264_4K_DEC count="1"/>
<H264_4K_INTERLACE_DEC count="1"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="1"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="1"/>
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="8" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="6" hw_enc="5" pip="3" reverse="6"/>
<BETA_TESTED_FLAG value="1"/>
</GPU>
<GPU name="Mali-T88">
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="-1"/>
<MPEG4_FWVGA_DEC count="5"/>
<H264_FWVGA_DEC count="5"/>
<H264_FWVGA_INTERLACE_DEC count="5"/>
<MPEG4_720P_DEC count="5"/>
<H264_720P_DEC count="5"/>
<H264_720P_INTERLACE_DEC count="5"/>
<MPEG4_1080P_DEC count="5"/>
<H264_1080P_DEC count="5"/>
<H264_1080P_INTERLACE_DEC count="5"/>
<H264_2K_DEC count="1"/>
<H264_2K_INTERLACE_DEC count="1"/>
<H264_4K_DEC count="1"/>
<H264_4K_INTERLACE_DEC count="1"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="1"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="1"/>
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="8" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="6" hw_enc="5" pip="3" reverse="6"/>
<BETA_TESTED_FLAG value="0"/>
</GPU>
<GPU name="Mali-T">
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="-1"/>
<MPEG4_FWVGA_DEC count="2"/>
<H264_FWVGA_DEC count="2"/>
<H264_FWVGA_INTERLACE_DEC count="2"/>
<MPEG4_720P_DEC count="2"/>
<H264_720P_DEC count="2"/>
<H264_720P_INTERLACE_DEC count="2"/>
<MPEG4_1080P_DEC count="2"/>
<H264_1080P_DEC count="2"/>
<H264_1080P_INTERLACE_DEC count="2"/>
<H264_2K_DEC count="1"/>
<H264_2K_INTERLACE_DEC count="1"/>
<H264_4K_DEC count="0"/>
<H264_4K_INTERLACE_DEC count="0"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="1"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="1"/>
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="8" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="6" hw_enc="6" pip="3" reverse="6"/>
<BETA_TESTED_FLAG value="0"/>
</GPU>
</GPU_List>
</serial>
<serial name="PowerVR">
<default_value>
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="-1"/>
<MPEG4_FWVGA_DEC count="2"/>
<H264_FWVGA_DEC count="2"/>
<H264_FWVGA_INTERLACE_DEC count="2"/>
<MPEG4_720P_DEC count="2"/>
<H264_720P_DEC count="2"/>
<H264_720P_INTERLACE_DEC count="2"/>
<MPEG4_1080P_DEC count="1"/>
<H264_1080P_DEC count="1"/>
<H264_1080P_INTERLACE_DEC count="1"/>
<H264_2K_DEC count="0"/>
<H264_2K_INTERLACE_DEC count="0"/>
<H264_4K_DEC count="0"/>
<H264_4K_INTERLACE_DEC count="0"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="1"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="1"/>
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="8" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="6" hw_enc="6" pip="3" reverse="6"/>
<BETA_TESTED_FLAG value="0"/>
</default_value>
<GPU_List count="4">
<GPU name="PowerVR SGX 531">
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="-1"/>
<MPEG4_FWVGA_DEC count="2"/>
<H264_FWVGA_DEC count="2"/>
<H264_FWVGA_INTERLACE_DEC count="2"/>
<MPEG4_720P_DEC count="2"/>
<H264_720P_DEC count="2"/>
<H264_720P_INTERLACE_DEC count="2"/>
<MPEG4_1080P_DEC count="0"/>
<H264_1080P_DEC count="0"/>
<H264_1080P_INTERLACE_DEC count="0"/>
<H264_2K_DEC count="0"/>
<H264_2K_INTERLACE_DEC count="0"/>
<H264_4K_DEC count="0"/>
<H264_4K_INTERLACE_DEC count="0"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="0"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="0"/>
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="8" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="6" hw_enc="6" pip="3" reverse="6"/>
<BETA_TESTED_FLAG value="0"/>
</GPU>
<GPU name="PowerVR SGX 540">
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="-1"/>
<MPEG4_FWVGA_DEC count="2"/>
<H264_FWVGA_DEC count="2"/>
<H264_FWVGA_INTERLACE_DEC count="2"/>
<MPEG4_720P_DEC count="2"/>
<H264_720P_DEC count="2"/>
<H264_720P_INTERLACE_DEC count="2"/>
<MPEG4_1080P_DEC count="1"/>
<H264_1080P_DEC count="1"/>
<H264_1080P_INTERLACE_DEC count="1"/>
<H264_2K_DEC count="0"/>
<H264_2K_INTERLACE_DEC count="0"/>
<H264_4K_DEC count="0"/>
<H264_4K_INTERLACE_DEC count="0"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="1"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="1"/>
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="8" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="6" hw_enc="6" pip="3" reverse="6"/>
<BETA_TESTED_FLAG value="0"/>
</GPU>
<GPU name="PowerVR SGX 544MP">
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="-1"/>
<MPEG4_FWVGA_DEC count="2"/>
<H264_FWVGA_DEC count="2"/>
<H264_FWVGA_INTERLACE_DEC count="2"/>
<MPEG4_720P_DEC count="2"/>
<H264_720P_DEC count="2"/>
<H264_720P_INTERLACE_DEC count="2"/>
<MPEG4_1080P_DEC count="1"/>
<H264_1080P_DEC count="1"/>
<H264_1080P_INTERLACE_DEC count="1"/>
<H264_2K_DEC count="0"/>
<H264_2K_INTERLACE_DEC count="0"/>
<H264_4K_DEC count="0"/>
<H264_4K_INTERLACE_DEC count="0"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="1"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="1"/>
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="8" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="6" hw_enc="6" pip="3" reverse="6"/>
<BETA_TESTED_FLAG value="0"/>
</GPU>
<GPU name="PowerVR Rogue G6200">
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="-1"/>
<MPEG4_FWVGA_DEC count="5"/>
<H264_FWVGA_DEC count="5"/>
<H264_FWVGA_INTERLACE_DEC count="5"/>
<MPEG4_720P_DEC count="5"/>
<H264_720P_DEC count="5"/>
<H264_720P_INTERLACE_DEC count="5"/>
<MPEG4_1080P_DEC count="5"/>
<H264_1080P_DEC count="5"/>
<H264_1080P_INTERLACE_DEC count="5"/>
<H264_2K_DEC count="1"/>
<H264_2K_INTERLACE_DEC count="1"/>
<H264_4K_DEC count="1"/>
<H264_4K_INTERLACE_DEC count="1"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="1"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="1"/>
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="8" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="6" hw_enc="5" pip="3" reverse="6"/>
<BETA_TESTED_FLAG value="1"/>
</GPU>
</GPU_List>
</serial>
<serial name="Immersion">
<default_value>
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="-1"/>
<MPEG4_FWVGA_DEC count="2"/>
<H264_FWVGA_DEC count="2"/>
<H264_FWVGA_INTERLACE_DEC count="2"/>
<MPEG4_720P_DEC count="2"/>
<H264_720P_DEC count="2"/>
<H264_720P_INTERLACE_DEC count="2"/>
<MPEG4_1080P_DEC count="1"/>
<H264_1080P_DEC count="1"/>
<H264_1080P_INTERLACE_DEC count="1"/>
<H264_2K_DEC count="0"/>
<H264_2K_INTERLACE_DEC count="0"/>
<H264_4K_DEC count="0"/>
<H264_4K_INTERLACE_DEC count="0"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="0"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="0"/>
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="8" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="6" hw_enc="6" pip="3" reverse="6"/>
<BETA_TESTED_FLAG value="0"/>
</default_value>
<GPU_List count="1">
<GPU name="Immersion.16">
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="-1"/>
<MPEG4_FWVGA_DEC count="2"/>
<H264_FWVGA_DEC count="2"/>
<H264_FWVGA_INTERLACE_DEC count="2"/>
<MPEG4_720P_DEC count="2"/>
<H264_720P_DEC count="2"/>
<H264_720P_INTERLACE_DEC count="2"/>
<MPEG4_1080P_DEC count="1"/>
<H264_1080P_DEC count="1"/>
<H264_1080P_INTERLACE_DEC count="1"/>
<H264_2K_DEC count="0"/>
<H264_2K_INTERLACE_DEC count="0"/>
<H264_4K_DEC count="0"/>
<H264_4K_INTERLACE_DEC count="0"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="0"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="0"/>
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="8" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="6" hw_enc="6" pip="3" reverse="6"/>
<BETA_TESTED_FLAG value="0"/>
</GPU>
</GPU_List>
</serial>
<serial name="VideoCore">
<default_value>
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="0"/>
<MPEG4_FWVGA_DEC count="2"/>
<H264_FWVGA_DEC count="2"/>
<H264_FWVGA_INTERLACE_DEC count="0"/>
<MPEG4_720P_DEC count="2"/>
<H264_720P_DEC count="2"/>
<H264_720P_INTERLACE_DEC count="0"/>
<MPEG4_1080P_DEC count="1"/>
<H264_1080P_DEC count="1"/>
<H264_1080P_INTERLACE_DEC count="0"/>
<H264_2K_DEC count="0"/>
<H264_2K_INTERLACE_DEC count="0"/>
<H264_4K_DEC count="0"/>
<H264_4K_INTERLACE_DEC count="0"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="0"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="0"/>
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="8" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="6" hw_enc="6" pip="3" reverse="6"/>
<BETA_TESTED_FLAG value="0"/>
</default_value>
<GPU_List count="1">
<GPU name="VideoCore IV HW">
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="0"/>
<MPEG4_FWVGA_DEC count="2"/>
<H264_FWVGA_DEC count="2"/>
<H264_FWVGA_INTERLACE_DEC count="0"/>
<MPEG4_720P_DEC count="2"/>
<H264_720P_DEC count="2"/>
<H264_720P_INTERLACE_DEC count="0"/>
<MPEG4_1080P_DEC count="1"/>
<H264_1080P_DEC count="1"/>
<H264_1080P_INTERLACE_DEC count="0"/>
<H264_2K_DEC count="0"/>
<H264_2K_INTERLACE_DEC count="0"/>
<H264_4K_DEC count="0"/>
<H264_4K_INTERLACE_DEC count="0"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="0"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="0"/>
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="8" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="6" hw_enc="6" pip="3" reverse="6"/>
<BETA_TESTED_FLAG value="0"/>
</GPU>
</GPU_List>
</serial>
<serial name="NVIDIA">
<default_value>
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="0"/>
<MPEG4_FWVGA_DEC count="2"/>
<H264_FWVGA_DEC count="2"/>
<H264_FWVGA_INTERLACE_DEC count="0"/>
<MPEG4_720P_DEC count="1"/>
<H264_720P_DEC count="1"/>
<H264_720P_INTERLACE_DEC count="0"/>
<MPEG4_1080P_DEC count="1"/>
<H264_1080P_DEC count="1"/>
<H264_1080P_INTERLACE_DEC count="0"/>
<H264_2K_DEC count="0"/>
<H264_2K_INTERLACE_DEC count="0"/>
<H264_4K_DEC count="0"/>
<H264_4K_INTERLACE_DEC count="0"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="1"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="1"/>
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="8" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="6" hw_enc="6" pip="3" reverse="6"/>
<BETA_TESTED_FLAG value="0"/>
</default_value>
<GPU_List count="1">
<GPU name="NVIDIA Tegra">
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="0"/>
<MPEG4_FWVGA_DEC count="2"/>
<H264_FWVGA_DEC count="2"/>
<H264_FWVGA_INTERLACE_DEC count="0"/>
<MPEG4_720P_DEC count="2"/>
<H264_720P_DEC count="2"/>
<H264_720P_INTERLACE_DEC count="0"/>
<MPEG4_1080P_DEC count="2"/>
<H264_1080P_DEC count="2"/>
<H264_1080P_INTERLACE_DEC count="0"/>
<H264_2K_DEC count="0"/>
<H264_2K_INTERLACE_DEC count="0"/>
<H264_4K_DEC count="0"/>
<H264_4K_INTERLACE_DEC count="0"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="1"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="1"/>
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="8" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="6" hw_enc="6" pip="3" reverse="6"/>
<BETA_TESTED_FLAG value="1"/>
</GPU>
</GPU_List>
</serial>
<serial name="Vivante">
<default_value>
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="0"/>
<MPEG4_FWVGA_DEC count="2"/>
<H264_FWVGA_DEC count="2"/>
<H264_FWVGA_INTERLACE_DEC count="0"/>
<MPEG4_720P_DEC count="1"/>
<H264_720P_DEC count="1"/>
<H264_720P_INTERLACE_DEC count="0"/>
<MPEG4_1080P_DEC count="0"/>
<H264_1080P_DEC count="0"/>
<H264_1080P_INTERLACE_DEC count="0"/>
<H264_2K_DEC count="0"/>
<H264_2K_INTERLACE_DEC count="0"/>
<H264_4K_DEC count="0"/>
<H264_4K_INTERLACE_DEC count="0"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="0"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="0"/>
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="3" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="6" hw_enc="6" pip="3" reverse="6"/>
<BETA_TESTED_FLAG value="0"/>
</default_value>
<GPU_List count="1">
<GPU name="Vivante GC2000">
<MPEG4_VGA_DEC count="-1"/>
<H264_VGA_DEC count="-1"/>
<H264_VGA_INTERLACE_DEC count="-1"/>
<MPEG4_FWVGA_DEC count="2"/>
<H264_FWVGA_DEC count="2"/>
<H264_FWVGA_INTERLACE_DEC count="0"/>
<MPEG4_720P_DEC count="1"/>
<H264_720P_DEC count="1"/>
<H264_720P_INTERLACE_DEC count="0"/>
<MPEG4_1080P_DEC count="0"/>
<H264_1080P_DEC count="0"/>
<H264_1080P_INTERLACE_DEC count="0"/>
<H264_2K_DEC count="0"/>
<H264_2K_INTERLACE_DEC count="0"/>
<H264_4K_DEC count="0"/>
<H264_4K_INTERLACE_DEC count="0"/>
<MPEG4_STANDARD_ENC value="0"/>
<H264_STANDARD_ENC value="0"/>
<MPEG4_UNSTANDARD_ENC value="0"/>
<H264_UNSTANDARD_ENC value="0"/>
<NORMAL_IMPORT_FORMAT sw_enc="3" hw_enc="3" pip="3" reverse="3"/>
<HD_IMPORT_FORMAT sw_enc="6" hw_enc="6" pip="3" reverse="6"/>
<BETA_TESTED_FLAG value="0"/>
</GPU>
</GPU_List>
</serial>
</GPU_Serial_List>
<MPEG4_DEC_UNSUPPORT_CPU_LIST count="1">
<item Implementer="0x41" Arch="7" Variant="0x0" Part="0xc07" Revision="4" gpu="Mali-400 MP"></item>
</MPEG4_DEC_UNSUPPORT_CPU_LIST>
<H264_DEC_UNSUPPORT_CPU_LIST count="1">
<item Implementer="0x41" Arch="7" Variant="0x0" Part="0xc07" Revision="4" gpu="Mali-400 MP"></item>
</H264_DEC_UNSUPPORT_CPU_LIST>
<MPEG4_ENC_UNSUPPORT_CPU_LIST count="0"></MPEG4_ENC_UNSUPPORT_CPU_LIST>
<H264_ENC_UNSUPPORT_CPU_LIST count="0"></H264_ENC_UNSUPPORT_CPU_LIST>
<MPEG4_DEC_UNSUPPORT_MODEL_LIST count="0"></MPEG4_DEC_UNSUPPORT_MODEL_LIST>
<H264_DEC_UNSUPPORT_MODEL_LIST count="0"></H264_DEC_UNSUPPORT_MODEL_LIST>
<MPEG4_ENC_UNSUPPORT_MODEL_LIST count="1">
<model name="M040"/>
</MPEG4_ENC_UNSUPPORT_MODEL_LIST>
<H264_ENC_UNSUPPORT_MODEL_LIST count="17">
<model name="M040"/>
<model name="LG-E980"/>
<model name="LG-F240"/>
<model name="LG-L-04E"/>
<model name="LG-E985"/>
<model name="LG-E986"/>
<model name="LG-E975"/>
<model name="LG-E973"/>
<model name="LG-E971"/>
<model name="LG-F180"/>
<model name="LG-E970"/>
<model name="IM-A860"/>
<model name="IM-A850"/>
<model name="IM-A870"/>
<model name="Moto X"/>
<model name="DROID Maxx"/>
<model name="XT1080"/>
</H264_ENC_UNSUPPORT_MODEL_LIST>
</root>
