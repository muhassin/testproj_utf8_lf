# testproj_utf8_lf

A test/example project to check how character sets/encodings and newlines get
handled by the development chain  (repository, git, IDE, local OS, settings).

This variant of the project is aimed for normal modern GIT projects, where
by default all text files are UTF-8 and use LF newlines (even locally on Windows
systems). Exceptions will be set explicitly in IDE and/or .editorconfig and/or
.gitattributes as necessary.

### IMPORTANT MANUAL SETUP

As files with exceptional charset/encoding (those not supported by editorconfig)
appear, add the instructions for them here, so that IDE can be made to handle
the charset/encoding.

* May need to ensure that all files are part of the IDE's project/module.
  (project's .iml is shared so that for this test project it is easier to do for IntelliJ Idea;
  if it doesn't happen automatically at import, just right click on the .iml file and use it...)
* In IntelliJ Idea, open File -> Settings... -> Editor -> File Encodings,
  check that the "Project Encoding" is explicitly set to UTF-8, or set it manually so.
* In the same place, ensure that src/win has encoding windows-1252.
* In the same place, ensure that default encoding for .properties files is iso-8859-1.

The windows-1252 being set in the IDE is important, because editorconfig
does not support that charset/encoding.


### Testing

Since most of normal project is done in a way that is being tested/checked
all the time around the world, the testing concentrates on checking the few
exceptional files.

1. Fork the project.
2. Clone the forked project (e.g. directly to Idea) for local work.
3. Create a new branch.
4. Check that the charset/encoding and newline formats match the filenames.
5. Make the explained changes in CRLF files. Commit them.
    * Especially check the .bat file newlines; seems Idea auto-converts them to LF
      on save, and an explicit conversion back to CRLF is needed. Also, on some versions
      of Idea, after that manual conversion to CRLF is done, Idea still shows LF on
      the status bar even though it is has actually been reverted correctly.
6. Create a new file in src/win (without explicitly setting the
   charset/encoding or newline format), add some ä ö in it, and after saving it,
   check the formats to be CP1252 and CRLF.
7. Recheck that the charset/encoding and newline formats match the filenames.
8. Push the new branch and its changes to your forked repository and create PR
   from the branch to main.
9. Check the shown diffs (note: do _not_ ignore whitespace...)

Any problems with charsets/encoding or converted newlines should be easily visible.
(Note, seems Github doesn't always handle cp1252/latin1 characters visually correctly
in diff-view, but the merge will still be done correctly. For example, the .bat file
with cp1252 is shown correctly, but the similar .txt file with cp1252 is not.)


### Other stuff

Note that this project does _not_ gitignore one file under .idea-directory; the encodings.xml file,
and the project's .iml file is also not gitignored for convenience.
