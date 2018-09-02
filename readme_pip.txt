easy_install -U pip
easy_install -U pip3

pip install --upgrade pip
pip list --outdated --format=freeze
sudo -H pip list --outdated --format=freeze

pip list --format=legacy --outdated | cut -d ' ' -f 1 | xargs -n 1 sudo -H pip install --upgrade
pip3 list --format=json --outdated | jq '.[] | .name' | xargs -n 1 sudo -H pip3 install --upgrade

