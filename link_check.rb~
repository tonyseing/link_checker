# command format is "ruby link_checker.rb [website] [output html file name]"

require 'rubygems'
require 'net/http'
require 'uri'
require 'anemone'

website = ARGV[0]
outputFile = ARGV[1]

def pageResponse(url)
  uri = URI.parse(url)
  response = nil
  Net::HTTP.start(uri.host, uri.port) { |http|
    response = http.head(uri.path.size > 0 ? uri.path : "/")
  }  
  if response.code == "200"
    "200 OK"
  elsif response.code == "201"
    "201 CREATED"
  elsif response.code == "202"
    "202 ACCEPTED"
  elsif response.code == "203"
    "203 PARTIAL INFORMATION"
  elsif response.code == "204"
    "203 NO RESPONSE"
  elsif response.code == "400"
    "400 BAD REQUEST"
  elsif response.code == "401"
    "401 UNAUTHORIZED"
  elsif response.code == "403"
    "400 FORBIDDEN"
  elsif response.code == "404"
    "404 PAGE NOT FOUND"
  elsif response.code == "500"
    "500 INTERNAL ERROR"
  elsif response.code == "301"
    "301 MOVED"
  elsif response.code == "302"
    "301 FOUND"
  elsif response.code == "304"
    "304 NOT MODIFIED"
  else   
    response.code
  end
  
end

myfile = File.open(outputFile.to_s, 'w') do |fileOut|
    Anemone.crawl(ARGV[0].to_s) do |anemone|
      anemone.on_every_page do |page|
	  puts "******" + page.url.to_s + "******"
	  fileOut.puts "<b>" + page.url.to_s + "</b><br/>"
	  
	  puts "---------------------------------"
	  fileOut.puts "---------------------------------<br/>"
	  
	  page.links.each do |link| 
	    puts link.to_s + " " + pageResponse(link.to_s).to_s
	    fileOut.puts link.to_s + " " + pageResponse(link.to_s).to_s + "<br/>"
	  end
	  fileOut.puts "<br/><br/>"
	  
      end
    end
end
