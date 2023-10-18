# Collaborative Development, Authoring and Publishing

The original workflow involved the main author providing PDF previews of the material to a second author by email, who returned an annotated and/or email comments.

OU-XML was also generated and passed to a DPA (Digital Production Assistant) in LDS (Learner and Discovery Services) who checked and fixed the OU-XML, published it as previewable content in the VLE, and provided errata about OU-XML issues to the main author.

As well as iterating the text in the source markdown documents, the main author was also iterating on the tools used to generate to the OU-XML. *This would not have been possible without the support of the DPA turning round documents almost on demand.*

Two recurring OU-XML issues were:

- unknown tags;
- incorrectly formatted or otherwise broken link references in internal reference links.

In parsing the markdown to Sphinx XML, various docutils XML tags were generated that were not recognised by the translation tool that converted Sphinx docutils XML to OU-XML.

Initially, and perhaps rather lazily, the main author passed this incorrect OU-XML to the DPA who then reported back the broken XML issues.

Several steps were then taken to improve this developmental workflow:

- the main author (working on an autonomous Mac) installed Microsoft Remote Desktop and via Citrix Secure Access and a Microsoft Authenticator app running providing 2FA from a  personal mobile phone, gained access to an OU configured Microsoft Desktop. This environment could then be used to run Oxygen XML Author application. After installing the OU Publishing extensions to Oxygen XML Author, the environment could then be used to:
  - validate the generated OU-XML against the OU-XML schema;
  - run additional quality checks against the generated OU-XML using unenforced Schematron quality rules; *these rules display quality improvement recommendations*
  - publish the content via a web browser to PDF or VLE previewed HTML.

```{admonition} Practical issues associated with using Oxygen XML Author

The default web browser in the Microsoft Desktop environment was an old browser that did not work properly when trying to run the OU-XML publisher. Changing Windows preferences to use Chrome fxed the issue. When rendering the OU-XML via the browser accessed web-service, OU authentication was required within each new RDP session, adding further friction to the process.
```

To simplify the process of validating the OU-XML, the XML schema file was located and exported. A simple OU-XML command line validation tool was then developed to allow for local validation of generated OU-XML files without the need to access Oxygen XML Author application. (The tool can be found [here](https://github.com/innovationOUtside/ou-xml-validator).) *A simple previewer XSL file also looked to be available for generating preview HTML from OU-XML.*

During the development process, the OU-XML schema was updated. This required updating both Oxygen XML Author and the OU-XML generator in line with the updated schema.

To try to improve the authoring/editing process, the first and second author started to use a public GitHub repository to share content. The second author forked the first author's repository, worked in their own repository, and then submitted pull requests back to the first author's repository.
