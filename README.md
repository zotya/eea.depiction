#  EEA Depiction

[![http://ci.eionet.europa.eu/job/eea.depiction-
www/badge/icon](https://camo.githubusercontent.com/fda576dea8933e9d2feab615f5f75451d60894ea/687474703a2f2f63692e65696f6e65742e6575726f70612e65752f6a6f622f6565612e646570696374696f6e2d7777772f62616467652f69636f6e)](http://ci.eionet.europa.eu/job/eea
.depiction-www/lastBuild) [![http://ci.eionet.europa.eu/job/eea.depiction-
plone4/badge/icon](https://camo.githubusercontent.com/4f73f7d5709350a22d7f0162f49cc6adf8d3833f/687474703a2f2f63692e65696f6e65742e6575726f70612e65752f6a6f622f6565612e646570696374696f6e2d706c6f6e65342f62616467652f69636f6e)](http://ci.eionet.europa.eu/job/eea
.depiction-plone4/lastBuild)

##  Introduction

[EEA Depiction](http://eea.github.com/docs/eea.depiction) (formerly
valentine.imagescales) is a generic system for creating thumbnails/image
representations for content types, both those provided by Plone, and custom
ones.

At the moment this system is implemented and tested only on Archetypes content
types, however this system could be adapted in a later version to work also
for dexterity content types.

To make it work for a content type, three adapters need to be provided:

  1. ImageView that retrieves an image in the desired scale.
  2. ImageTag that returns the HTML tag for the image
  3. ImageLink that returns the HTML link to the image.

##  Upgrade notes

As of **eea.depiction 5.2** we customize the following resources in order to
display any items in thumbnail listings:

  1. **atctListAlbum.py** \- which is responsible for displaying items in _atct_album_view.pt_
  2. **thumbnail_view.pt** \- which is the browser template responsible for thumbnail listing for the _plone.app.collection_ package

Contents

  * Introduction
  * Upgrade notes
  * Installation
  * How to specify fallback preview images
  * Dependencies
  * Source code
  * Copyright and license
  * Funding and project management

##  Installation

##  zc.buildout

If you are using [zc.buildout](http://pypi.python.org/pypi/zc.buildout) and
the
[plone.recipe.zope2instance](http://pypi.python.org/pypi/plone.recipe.zope2instance)
recipe to manage your project, you can do this:

  * Update your buildout.cfg file:

    * Add `eea.depiction` to the list of eggs to install
    * Tell the [plone.recipe.zope2instance](http://pypi.python.org/pypi/plone.recipe.zope2instance) recipe to install a ZCML slug
    
        [instance]
    ...
    eggs =
      ...
      eea.depiction
    
    zcml =
      ...
      eea.depiction-overrides
      eea.depiction
    

  * Re-run buildout, e.g. with:
    
        $ ./bin/buildout
    

You can skip the ZCML slug if you are going to explicitly include the package
from another package's configure.zcml file.

##  How to specify fallback preview images

eea.depiction 0.3 introduces the concept of fallback images when the regular
image traversal fails. The logic works like this:

  1. Look for an image returned by the contexts 'imgview' adapter
  2. If the imgview crashes, isn't found or can not locate/generate an image, we continue by checking if there's an image specified for any of the contexts interfaces.
  3. If there's no fallback image, we look for an image for the context portal type, e.g. article, news-item, document. This should be placed in the 'portal_depiction' utility (Site Setup &gt; Depiction Library)
  4. Uses the generic content type image, i.e. portal_depiction/generic

Thus:

  1. To map a fallback image to a portal type, place it in this folder and name it after the portal type.
  2. To map a fallback image to an interface just add a named-utility for IDepictionVocabulary (see eea.depiction.vocabularies)

##  Dependencies

[EEA Depiction](http://eea.github.com/docs/eea.depiction) has the following
dependencies:

    

  * Plone 4+
  * Pillow

This package also supports p4a.video. Thus the following dependencies are
optional:

    

  * p4a.video

    
    
    [instance]
    ...
    eggs =
      ...
      eea.depiction [full]
    

##  Source code

Latest source code (Plone 4 compatible):

    

  * <http://github.com/eea/eea.depiction>
  * <http://github.com/collective/eea.depiction>

##  Copyright and license

The Initial Owner of the Original Code is European Environment Agency (EEA).
All Rights Reserved.

The eea.depiction (the Original Code) is free software; you can redistribute
it and/or modify it under the terms of the GNU General Public License as
published by the Free Software Foundation; either version 2 of the License, or
(at your option) any later version.

More details under docs/License.txt

##  Funding and project management

[EEA](http://www.eea.europa.eu/) \- European Environment Agency (EU)

