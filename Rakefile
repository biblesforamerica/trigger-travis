require 'travis'

desc "Builds the branch ENV['TRAVIS_BRANCH'] for repository ENV['TRAVIS_REPOSITORY'] with token ENV['GITHUB_TOKEN']"

task :build do
  pro = ENV['TRAVIS_PRO']
  token = ENV['GITHUB_TOKEN']
  repo = ENV['TRAVIS_REPOSITORY']
  branch = ENV['TRAVIS_BRANCH']

  if pro
    client = Travis::Client.new('https://api.travis-ci.com')
  else
    client = Travis::Client.new
  end

  client.github_auth(token)

  repo_name = repo.gsub(/\//, '%2F')
  url = "/repo/#{repo_name}/requests"
  body = {
    request: {
      branch: branch,
      message: "Nightly build of branch #{branch} via Heroku.",
    },
  }
  headers = {
    'Travis-API-Version' => 3,
  }

  client.post_raw(url, body, headers)
end
