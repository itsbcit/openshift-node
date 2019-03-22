require "erb"

# @ripienaar https://www.devco.net/archives/2010/11/18/a_few_rake_tips.php
# Brilliant.
def render_template(template, output, scope)
    tmpl = File.read(template)
    erb = ERB.new(tmpl, 0, "<>")
    File.open(output, "w") do |f|
        f.puts erb.result(scope)
    end
end

desc "Update Dockerfile templates"
task :default do

  maintainer = 'jesse@weisner.ca, chriswood.ca@gmail.com'
  org_name = 'bcit'
  image_name = 'openshift-node'
  alpinetag = '3.9'
  nodever = '11.12.0'
  yarnver = '1.15.2'
  tags = [
    '11'
  ]

  tags.each do |tag|
      sh "mkdir -p #{tag}"
      render_template("Dockerfile.erb", "#{tag}/Dockerfile", binding)
      Dir.chdir(tag) do
        sh "docker build -t #{org_name}/#{image_name}:#{tag} ."
        #sh "docker push #{org_name}/#{image_name}:#{tag}"
      end
  end
end
