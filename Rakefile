# coding: utf-8
require 'find'
require 'jekyll'
require 'tinify'
require 'pry'

config_file = '_config.yml' # Name of Jekyll config file

def fetch_jekyll_config(config_file)
  site = Jekyll::Configuration.new
  site.read_config_file(config_file)
end

site_configuration = fetch_jekyll_config(config_file)

task :image_compress do
  # Read in directories for `_config.yml`
  source_dir = site_configuration['tinypng_src_dir']
  dest_dir = site_configuration['tinypng_dest_dir']
  images_to_compress = find_images_to_compress(source_dir, dest_dir)
  tinify_images(images_to_compress, dest_dir)
end

#### Misc Methods
def find_files_in_directory(directory)
  files = {}
  Find.find(directory) do |path|
    if File.file?(path)
      relative_path = path[directory.length, path.length]
      files[relative_path] = path
    end
  end
  files
end

def find_images_to_compress(source_dir, dest_dir)
  # Only compress images that have not already been compressed.
  src_files = find_files_in_directory(source_dir)
  dst_files = find_files_in_directory(dest_dir)
  results = src_files.keys - dst_files.keys
  images = {}
  results.each do |result|
    images[result] = src_files[result]
  end
  images
end

def tinify_images(images, dest_dir)
  Tinify.key = ENV['TINYPNG_API_KEY']
  binding.pry
  images.each do |k, v|
    puts 'Compressing image: ' + v
    source = Tinify.from_file(v)
    source.to_file(File.join(dest_dir, k))
  end
rescue => e
  puts 'Something related to Tinify blew up: ' + e.message
end