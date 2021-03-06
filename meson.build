project('com.github.muriloventuroso.easyssh', 'vala', 'c', version: '1.6.6')

gnome = import('gnome')
i18n = import('i18n')
with_gpg = get_option('with-gpg')
add_global_arguments('-DGETTEXT_PACKAGE="@0@"'.format(meson.project_name()), language:'c')

if get_option('ubuntu-bionic-patched-vte')
    add_project_arguments(['--define', 'UBUNTU_BIONIC_PATCHED_VTE'], language : 'vala')
endif

asresources = gnome.compile_resources(
    'as-resources', 'data/' + meson.project_name() + '.gresource.xml',
    source_dir: 'data',
    c_name: 'as'
)


dependencies = [
    dependency('gee-0.8'),
    dependency('glib-2.0'),
    dependency('gtk+-3.0'),
    dependency('granite'),
    dependency('json-glib-1.0'),
    dependency('vte-2.91', version: '>0.52'),
    dependency('gee-0.8'),
    meson.get_compiler('c').find_library('m', required : false)
]
if get_option('libunity')
    unity_dep = dependency('unity')
    add_project_arguments('--define=UNITY_SUPPORT=1', language : 'vala')
    dependencies += unity_dep
endif

if with_gpg
    gpg = find_program('gpg', 'gpg2', required: true)
    add_project_arguments(['--define', 'WITH_GPG'], language : 'vala')

endif



executable(
    meson.project_name(),
    asresources,
    'src/Application.vala',
    'src/Host.vala',
    'src/Account.vala',
    'src/Bookmark.vala',
    'src/MainWindow.vala',
    'src/Services/Settings.vala',
    'src/Views/SourceListView.vala',
    'src/Widgets/TerminalBox.vala',
    'src/Widgets/Welcome.vala',
    'src/Widgets/WelcomeAccounts.vala',
    'src/Widgets/HeaderBar.vala',
    'src/Widgets/ConnectionEditor.vala',
    'src/Widgets/AccountEditor.vala',
    'src/Widgets/Connection.vala',
    'src/Widgets/ErrorRevealer.vala',
    'src/Widgets/Preferences.vala',
    'src/Widgets/TerminalWidget.vala',
    'src/Widgets/SearchToolbar.vala',
    'src/Widgets/BookmarksPopover.vala',
    'src/Widgets/Tab.vala',
    dependencies: dependencies,
    install: true
)

meson.add_install_script('meson/post_install.py')

subdir('data')
subdir('po')