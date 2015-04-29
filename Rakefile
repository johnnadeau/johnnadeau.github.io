# adapted from https://github.com/imathis/octopress/blob/master/Rakefile   
# usage rake post:new -title="Awesome Blog Post" or rake post:new (defaults to "My New Post")
namespace :post do
  desc "Start a new post"
  task :new  do 
    title = ENV["title"] || "My New Post"
    filename = "_posts/#{Time.now.strftime('%Y-%m-%d')}-#{title.downcase.gsub(/&/,'and').gsub(/[,'":\?!\(\)\[\]]/,'').gsub(/[\W\.]/, '-').gsub(/-+$/,'')}.markdown"
    puts "Creating new post: #{filename}"
    open(filename, 'w') do |post|
      system "mkdir -p _posts";
      post.puts "---"
      post.puts "layout: post"
      post.puts "title: \"#{title.gsub(/&/,'&amp;')}\""
      post.puts "date: #{Time.now.strftime('%Y-%m-%d %H:%M')}"
      post.puts "published: false"
      post.puts "tags: " 
      post.puts "comments: true"
      post.puts "---"
    end
  end
end
