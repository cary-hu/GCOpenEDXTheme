tutor local run lms -d --extra-volumes "$PWD:/openedx/themes" bash -c "cd /openedx/themes/GCOpenEDXTheme && paver watch_assets lms --settings=tutor.production"


tutor dev run lms --extra-vars "EDXAPP_EXTRA_ENV_SETTINGS=lms.env.json EDXAPP_LMS_BASE_THEME=GCOpenEDXTheme DJANGO_SETTINGS_MODULE=lms.envs"

tutor local start lms --mount "lms:$PWD:/openedx/themes/GCOpenEDXTheme"

echo "EDXAPP_THEME=GCOpenEDXTheme" > "$(tutor config printroot)/env/dev"

tutor local start --mount "lms:$PWD:/openedx/themes/GCOpenEDXTheme" bash -c "cd /openedx/themes/GCOpenEDXTheme && paver watch_assets lms --settings=tutor.production"

