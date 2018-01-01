---
layout: post
title: Prawn VS Wicked PDF
category: code
tags: pdf rails
---

From time to time, we all have to work with PDF. Which third party library do you use to generate PDF in Rails? 

<!--more-->

* TOC
{:toc}

## Prawn

One of the famous pdf generating systems in Ruby community is [Prawn](https://github.com/prawnpdf/prawn), also featured in [RailsCasts Ep153](http://railscasts.com/episodes/153-pdfs-with-prawn). 

As the gem stated:
> If you are looking for a highly flexible PDF document generation system, Prawn might be the tool for you. It is not a reporting tool or a publishing toolchain, though it could be fairly easily used to build those things.

Prawn works more like a Microsoft Paint. It has a coordinate system, which means you could literally place a piece of data anywhere you want in the page. If you are not a fan of HTML's positioning system, or try to fill in a prepared form, Prawn might be a better solution. It also has a great [manual](http://prawnpdf.org/manual.pdf), loaded with lots of real world examples.

### Set up

#### Dependencies

1. `gem install 'prawn'`
2. `require 'prawn'` in your initializer, e.g. `/config/initializers/prawn.rb`

#### Sample service class

Below is a pseudo service class for how to generating pdf using Prawn:

    class OrderPdf < Prawn::Document
      def initialize(options = {})
        super
        @order = options[:order]
        @customer = @order.user
        @products = @order.products
        build_logo
        build_basic
        build_product
      end
        
      def build_logo
        image open('https://www.example.com/example-logo.png'), at: [0, 500], scale: 0.15
      end
        
      def build_basic
        # Helper for printing the coordinate to pdf, make it much easier
        # to position certain text, especially with prepared form
        # stroke_axis(at: [50, 150], height: 50, step_length: 2,
        #             negative_axes_length: 5, color: '0000FF')
        draw_text "Order ID #{@order.id} for #{@customer.name}", at: [0, 450], size: 9
      end
      
      ...
    end

## Wicked PDF

If you are looking for converting a html page to pdf. There are couple of libraries available to you, such as [Prince](http://www.princexml.com/), [wkhtmltopdf](https://wkhtmltopdf.org/) and etc. The first one is a paid service, which cost $3,800 for a server license and $495 for desktop use. On the other hand, wkhtmltopdf is a free open source command line tools using the Qt WebKit rendering engine.

For personal and small business use, wkhtmltopdf is the obvious winner.

After the installation, it is simple as `wkhtmltopdf http://google.com google.pdf`.

There are two gems based on wkhtmltopdf cli, [pdfkit](https://github.com/pdfkit/pdfkit) and [Wicked PDF](https://github.com/mileszs/wicked_pdf). Wicked PDF is suggested to me as it handles dependence better. So I went with it, and am pretty happy with the decision.

### Set up

#### Dependencies

1. Install both wicked pdf and wkhtmltopdf in Rails using `gem 'wicked_pdf'; gem 'wkhtmltopdf-binary'`

2. Use `rails generate wicked_pdf` to generate the initializer. And you need to config the path of cli in initializer for production server, so Rails know where to find the wkhtmltopdf library.
    
        WickedPdf.config = {
          exe_path: '/usr/local/bin/wkhtmltopdf'
        }

#### Set your parameters in controller

Make sure you provide the absolute path for template to make the code work. 

    format.pdf do
      render pdf: 'Things.pdf',
             locals: { things: @things },
             disposition: 'inline',
             template: 'admin/things/show.pdf.erb',
             show_as_html: true,
             margin: { top: 10,
                       bottom: 10,
                       left: 0,
                       right: 0 }
    end

#### Prepare HTML template

Think of this HTML template as a separate layout from `application.html.erb`, and wkhtmltopdf does not know anything about your Rails app. 

    <!doctype html>
    <html>
      <head>
        <meta charset='utf-8' />
        <!-- Include Bootstrap separately due to url recognition -->
        <!-- ref: https://github.com/mileszs/wicked_pdf/issues/470 -->
        <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" integrity="sha384-BVYiiSIFeK1dGmJRAkycuHAHRg32OmUcww7on3RYdg4Va+PmSTsz/K68vbdEjh4u" crossorigin="anonymous">
        <%= wicked_pdf_stylesheet_link_tag 'things' %>
        <%= wicked_pdf_javascript_include_tag 'things' %>
      </head>
      <body>
        <div class="container">
          <div class="row">
            <!-- Switch to col-xs for better print effect -->
            <div class="col-xs-6">
              <%= wicked_pdf_image_tag 'logo.png', class: 'img-responsive' %>
            </div>
            <div class="col-xs-6">
              <p>Things</p>
            </div>
          </div>
        </div>
      </body>
    </html>

#### Include asset
    
Include the `thing.js` and `thing.scss` in the pre-compile asset, ref to [clarification on usage with asset pipeline?](https://github.com/mileszs/wicked_pdf/issues/257) for more details. 

E.g. in `asset.rb`:
    
    Rails.application.config.assets.precompile += %w(thing.js thing.scss)

#### Catch on updated features on CSS

If you are a fan of flexbox like me, there is a catch on Flexbox. As explained by [npinchot](https://github.com/wkhtmltopdf/wkhtmltopdf/issues/1522)

    > wkhtmltopdf uses Qt to render HTML. The current version of wkhtmltopdf uses Qt 4.8.5, which uses version 2.2.4 of WebKit, so unfortunately flex box is not fully supported. It is partially supported with an older syntax.
    
The solution for this is to use the old syntax of flexbox, which is the syntax used in version 2.2.4 of WebKit.

---

*Reference*

1. [Mike Ackerman - How To Create PDFs in Rails](https://www.viget.com/articles/how-to-create-pdfs-in-rails)

2. [Andreas Happe - Generating PDFs from Ruby on Rails](https://www.snikt.net/blog/2012/04/26/wicked-pdf/)




