def ensure_git_branch_is_master
  branch = `git branch --no-color`.split("\n").grep(/^\* /).first[2..-1]
  raise "must be on master branch" unless branch == 'master'
end

def ensure_git_pristine
  status = `git status --porcelain`.strip
  raise "uncommitted changes! aborting!" if status.length > 0
  
  sh "git fetch origin"
  
  sha1_local = `git rev-parse master`.strip
  sha1_remote = `git rev-parse remotes/origin/master`.strip
  raise "unmerged changes between local and origin" unless sha1_local == sha1_remote
end

def create_tag(tag)
  sh "git commit -a -m '#{tag}'"
  sh "git tag -a -m '#{tag}' b#{tag}"
  sh "git push origin master tag b#{tag}"
end

task(:ensure_git_branch_is_master) { ensure_git_branch_is_master }
task(:ensure_git_pristine) { ensure_git_pristine }

