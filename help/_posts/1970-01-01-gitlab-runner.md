---
category: help
layout: help
mirrorid: gitlab-runner
---

# GitLab Runner 软件仓库镜像使用帮助

<form class="form-inline">
<div class="form-group">
	<label>是否使用 HTTPS</label>
	<select id="http-select" class="form-control content-select" data-target="#content-0,#content-1,#content-2,#content-3,#content-4">
	  <option data-http_protocol="https://" selected>是</option>
	  <option data-http_protocol="http://">否</option>
	</select>
</div>
</form>


<form class="form-inline">
<div class="form-group">
	<label>是否使用 sudo</label>
	<select id="sudo-select" class="form-control content-select" data-target="#content-0,#content-1,#content-2,#content-3,#content-4">
	  <option data-sudo="sudo " selected>是</option>
	  <option data-sudo="">否</option>
	</select>
</div>
</form>



**注意：gitlab-runner 镜像支持 x86-64 和 ARM64(aarch64) 架构**

### Debian/Ubuntu 用户

首先信任 GitLab 的 GPG 公钥：



{% raw %}
<script id="template-0" type="x-tmpl-markup">
curl https://packages.gitlab.com/gpg.key 2> /dev/null | {{sudo}}apt-key add - &>/dev/null
</script>
{% endraw %}

<p></p>

<pre>
<code id="content-0" class="language-bash" data-template="#template-0" data-select="#http-select,#sudo-select">
</code>
</pre>


再选择你的 Debian/Ubuntu 版本，文本框中内容写进 `/etc/apt/sources.list.d/gitlab-runner.list`



<form class="form-inline">
<div class="form-group">
  <label>发行版：</label>
    <select id="select-1-0" class="form-control content-select" data-target="#content-1">
      <option data-os_name="debian" data-release_name="bullseye" selected>Debian 11</option>
      <option data-os_name="debian" data-release_name="buster">Debian 10</option>
      <option data-os_name="debian" data-release_name="stretch">Debian 9</option>
      <option data-os_name="debian" data-release_name="jessie">Debian 8</option>
      <option data-os_name="ubuntu" data-release_name="jammy">Ubuntu 22.04 LTS</option>
      <option data-os_name="ubuntu" data-release_name="focal">Ubuntu 20.04 LTS</option>
      <option data-os_name="ubuntu" data-release_name="bionic">Ubuntu 18.04 LTS</option>
      <option data-os_name="ubuntu" data-release_name="xenial">Ubuntu 16.04 LTS</option>
    </select>
</div>
</form>

{% raw %}
<script id="template-1" type="x-tmpl-markup">
deb {{http_protocol}}{{mirror}}/{{os_name}} {{release_name}} main
</script>
{% endraw %}

<p></p>

<pre>
<code id="content-1" class="language-properties" data-template="#template-1" data-select="#http-select,#sudo-select,#select-1-0">
</code>
</pre>



安装 gitlab-runner:



{% raw %}
<script id="template-2" type="x-tmpl-markup">
{{sudo}}apt-get update
{{sudo}}apt-get install gitlab-runner
</script>
{% endraw %}

<p></p>

<pre>
<code id="content-2" class="language-bash" data-template="#template-2" data-select="#http-select,#sudo-select">
</code>
</pre>


### CentOS/RHEL

新建 `/etc/yum.repos.d/gitlab-runner.repo`，内容为




{% raw %}
<script id="template-3" type="x-tmpl-markup">
[gitlab-runner]
name=gitlab-runner
baseurl={{http_protocol}}{{mirror}}/yum/el$releasever-$basearch/
repo_gpgcheck=0
gpgcheck=0
enabled=1
gpgkey=https://packages.gitlab.com/gpg.key
</script>
{% endraw %}

<p></p>

<pre>
<code id="content-3" class="language-ini" data-template="#template-3" data-select="#http-select,#sudo-select">
</code>
</pre>


再执行



{% raw %}
<script id="template-4" type="x-tmpl-markup">
{{sudo}}yum makecache
{{sudo}}yum install gitlab-runner
</script>
{% endraw %}

<p></p>

<pre>
<code id="content-4" class="language-bash" data-template="#template-4" data-select="#http-select,#sudo-select">
</code>
</pre>


