JUnit5 Docset
=======================

* Docset generated by: maenujem https://github.com/maenujem
* Source docs: https://junit.org/junit5/docs/current/api/
* How to generate (Ubuntu-Linux):
```
# download docs
wget --recursive --page-requisites --convert-links --no-parent https://junit.org/junit5/docs/current/api/
cd junit.org/junit5/docs/current/api
# create distribution-directory
mkdir JUnit5
# workaround index-files/-paths: ../ is required to navigate in pages but not in generated docset-index (see also 'package and cleanup')w
cp index-files index-files_sav
sed -i -- 's|\.\.\/||gp' index-files/index-*.html
# generate structure, docSet.dsidx and info.plist using docker-image containing go (required for javadocset-script)
docker run -it --rm -v junit.org/junit5/docs/current/api:/go/src/junit5 golang
go get github.com/william8th/javadocset
javadocset JUnit5 src/junit5
mv JUnit5.docset/ src/junit5/JUnit5
exit
sudo chown -R user:user JUnit5/JUnit5.docset/
# add icons and infos
add icons to JUnit5/JUnit5.docset/
add docset.json and README.md to JUnit5/
# package and cleanup -> push to git-repo
rm -r JUnit5/JUnit5.docset/Contents/Resources/Documents/index-files
mv JUnit5/JUnit5.docset/Contents/Resources/Documents/index-files_sav JUnit5/JUnit5.docset/Contents/Resources/Documents/index-files
tar -cvzf JUnit5.tgz JUnit5/JUnit5.docset/
rm - r JUnit5/JUnit5.docset/
```
Logo was generated from the JUnit logo at https://junit.org/junit5/
