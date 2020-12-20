require 'net/http'
require 'nokogiri'

# Validates the url to be valid in case of invalid url return false else return true
def validate_custom_url(url)
    uri = URI.parse(url)
    uri.is_a?(URI::HTTP) && !uri.host.nil?
    rescue URI::InvalidURIError
    false
end

# Accepts a url Recieves response and returns parsed html content.
def get_parsedhtml_content(url)
    uri = URI(url)
    recieved_response = Net::HTTP.get(uri) 
    Nokogiri::HTML(recieved_response)
end

# Recieves the parsed content and filters the image tags sources
def get_available_images_from_parsed_content(url)
    get_parsedhtml_content(url).xpath('.//img/@src').map {|image| p image.value}
end

# Rake task that prints the available images from the provided url
desc 'image_scraper'
task :custom_scraper, [:url] do |t, args|
    web_url = args[:url]
    
    p "Executing the image scraper #{t}"
    if validate_custom_url(web_url)
        available_images = get_available_images_from_parsed_content(web_url)
    else
        p "The url specified seems to be invalid"
    end
    p  "There are no images in the website specified" unless available_images.count > 0 
end
