# adapted from https://github.com/imathis/octopress/blob/master/Rakefile   
# usage rake new_post['My New Post'] or rake new_post (defaults to "My New Post")
desc "Start a new post"
task :new_post, :title do |t, args|
  args.with_defaults(:title => 'My New Post')
  title = args.title
  filename = "_posts/#{Time.now.strftime('%Y-%m-%d')}-#{title.downcase.gsub(/&/,'and').gsub(/[,'":\?!\(\)\[\]]/,'').gsub(/[\W\.]/, '-').gsub(/-+$/,'')}.markdown"
  puts "Creating new post: #{filename}"
  open(filename, 'w') do |post|
    system "mkdir -p _posts";
    post.puts "---"
    post.puts "layout: post"
    post.puts "title: \"#{title.gsub(/&/,'&amp;')}\""
    post.puts "date: #{Time.now.strftime('%Y-%m-%d %H:%M')}"
    post.puts "published: false"
    post.puts "---"
  end
end
