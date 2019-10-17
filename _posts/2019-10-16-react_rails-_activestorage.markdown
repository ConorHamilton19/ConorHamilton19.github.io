---
layout: post
title:      "React/Rails- ActiveStorage"
date:       2019-10-17 03:01:29 +0000
permalink:  react_rails-_activestorage
---


Since the upgrade to Rails 5.2 saving and managing files and images with a database and ActiveRecord has become somewhat more streamlined due to the addition of ActiveStorage. Not to say that it is a straight forward process by any means but the pieces are now all included to help cut down on third party gems and other work arounds.

From the Rails Guide:

*What is Active Storage?
Active Storage facilitates uploading files to a cloud storage service like Amazon S3, Google Cloud Storage, or Microsoft Azure Storage and attaching those files to Active Record objects. It comes with a local disk-based service for development and testing and supports mirroring files to subordinate services for backups and migrations.*

If you are looking to figure out how to install and use basic ActiveStorage, you can find that here:             [https://edgeguides.rubyonrails.org/active_storage_overview.html](http://)

The above guide is a good first step into using ActiveStorage within a Rails application, what I found to be a little more difficult was taking an image that was input in a React JS form, store it in your rails backend database and then display that image back in React front-end land. Where this gets confusing is that ActiveStorage though similar to tables and relations in ActiveRecord, has a lot more going on under the hood. The API on it describes it as such ;

*A key difference to how Active Storage works compared to other attachment solutions in Rails is through the use of built-in Blob and Attachment models (backed by Active Record). This means existing application models do not need to be modified with additional columns to associate with files. Active Storage uses polymorphic associations via the Attachment join model, which then connects to the actual Blob.

*Blob models store attachment metadata (filename, content-type, etc.), and their identifier key in the storage service. Blob models do not store the actual binary data. They are intended to be immutable in spirit. One file, one blob. You can associate the same blob with multiple application models as well. And if you want to do transformations of a given Blob, the idea is that you'll simply create a new one, rather than attempt to mutate the existing one (though of course you can delete the previous version later if you don't need it).*

Thats a lot of words to say that through some meta-programming it relates your models to the image(as an attachment and a blob). This means that without even adding another collumn to your table that the image will be available to that class. But with all of this comes some pretty specific ways needed to go about sending an ASYNC POST and GET requests to store this image in the database and bring it back to the Store.

1) Follow steps in rails guide to set up ActiveStorage locally.

2) The image and metadata needs to be appended to a FormData() object when the form is filled out and submitted in React. I used the DropZone library to upload photos into form. [https://www.dropzonejs.com
](http://)


```
    const photo = new FormData()
    photo.append('[photo]title', this.state.photo.title)
    photo.append('[photo]owner', this.state.photo.owner)
    photo.append('[photo]picture', this.state.photo.picture)
```
 
 Fairly simple, when my react form is submitted I take the information that was added to the state and append it to a FormData object, including the image.
 
 3) The ASYNC POST request needs to have no headers and the FormData should be the only thing in the body.
 
```
  return fetch(`http://localhost:3000/api/v1/photos`, {
    method: 'POST',
    body: photo
		})
```
				
 This allows ActiveStorage to take over from here without limiting what is acceptable to send.
 
 4) The image stored in the Rails db now needs to be serialized so that React can understand it and pull the URL out to display the image.
 
```
class PhotoSerializer < ActiveModel::Serializer
  include Rails.application.routes.url_helpers

attributes :id, :title, :owner, :vote_count, :picture

def picture
  return unless object.picture.attached?

  object.picture.blob.attributes
        .slice('filename', 'byte_size')
        .merge(url: picture_url)
        .tap { |attrs| attrs['name'] = attrs.delete('filename') }
end

def picture_url
  url_for(object.picture)
end

end
```

Getting this to work can be fairly tricky. The environment file needs to be set up properly to use url_helpers. Make sure to restart your server once environment file is edited. 

From here the image should be in the proper form to ready to be used with an image tag with the src being the url that you serialized into the proper format.

Please take a look at how I was able to get this working if you have any questions. https://github.com/ConorHamilton19/pic-the-best-pic

![](https://media.giphy.com/media/11sBLVxNs7v6WA/source.gif)
 


