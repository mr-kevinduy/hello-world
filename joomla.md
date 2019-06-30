
## Licycle Joomla
ROOT = ~
1. Front Site:

```sh
    - ~/index.php
        - ~/includes/defines.php - CONSTANT VARIABLES.
        - ~/includes/framework.php - Include joomla framework.
            - ~/libraries/import.legacy.php
                - ~/libraries/loader.php - abstract class JLoader
                JLoader::setup();
                    spl_autoload_register(array('JLoader', 'load'));

                    // Register the J prefix and base path for Joomla platform libraries.
                    self::registerPrefix('J', JPATH_PLATFORM . '/joomla');
                    // Register the prefix autoloader.
                    spl_autoload_register(array('JLoader', '_autoload'));

                    spl_autoload_register(array('JLoader', 'loadByPsr0'));
                    spl_autoload_register(array('JLoader', 'loadByPsr4'));
                    spl_autoload_register(array('JLoader', 'loadByAlias'));


                JLoader::registerPrefix('J', JPATH_PLATFORM . '/legacy');
                JLoader::register('JsonSerializable', JPATH_PLATFORM . '/vendor/joomla/compat/src/JsonSerializable.php');
                // Register the PasswordHash lib
                JLoader::register('PasswordHash', JPATH_PLATFORM . '/phpass/PasswordHash.php');

                // Register classes where the names have been changed to fit the autoloader rules
                // @deprecated  4.0
                JLoader::register('JSimpleCrypt', JPATH_PLATFORM . '/legacy/simplecrypt/simplecrypt.php');
                JLoader::register('JTree', JPATH_PLATFORM . '/legacy/base/tree.php');
                JLoader::register('JNode', JPATH_PLATFORM . '/legacy/base/node.php');
                JLoader::register('JObserver', JPATH_PLATFORM . '/legacy/base/observer.php');
                JLoader::register('JObservable', JPATH_PLATFORM . '/legacy/base/observable.php');
                JLoader::register('LogException', JPATH_PLATFORM . '/legacy/log/logexception.php');
                JLoader::register('JXMLElement', JPATH_PLATFORM . '/legacy/utilities/xmlelement.php');
                JLoader::register('JCli', JPATH_PLATFORM . '/legacy/application/cli.php');
                JLoader::register('JDaemon', JPATH_PLATFORM . '/legacy/application/daemon.php');
                JLoader::register('JApplication', JPATH_LIBRARIES . '/legacy/application/application.php');

            - ~/libraries/cms.php
                - Check if JLoader not exits -> import ~/libraries/loader.php - abstract class JLoader
                // Register the library base path for CMS libraries.
                JLoader::registerPrefix('J', JPATH_PLATFORM . '/cms', false, true);

                /** @note This will be loaded through composer in Joomla 4 */
                JLoader::registerNamespace('Joomla\\CMS', JPATH_PLATFORM . '/src', false, false, 'psr4');

                // Create the Composer autoloader
                $loader = require JPATH_LIBRARIES . '/vendor/autoload.php';
                $loader->unregister();

                // Decorate Composer autoloader
                spl_autoload_register(array(new JClassLoader($loader), 'loadClass'), true, true);

                // Register the class aliases for Framework classes that have replaced their Platform equivilents
                require_once JPATH_LIBRARIES . '/classmap.php';
                    - Giải thích 1 vài namespace trước khi vào nội dung của file `classmap.php` này:
                    '\\Joomla\\CMS\\' : ~/libraries/src/
                    '\\Joomla\\Registry\\' : ~/libraries/vendor/joomla/registry/src/
                    '\\Joomla\\String\\' : ~/libraries/vendor/joomla/string/src/
                    '\\Joomla\\Data\\' : ~/libraries/vendor/joomla/data/src/
                    ...

                    - Nội dung file `classmap.php`:
                    JLoader::registerAlias('JRegistry', '\\Joomla\\Registry\\Registry', '5.0'); // ~/libraries/vendor/composer/autoload_classmap : 'Joomla\\Registry\\Registry' => '~/libraries/vendor/joomla/registry/src/Registry.php'

                    JLoader::registerAlias('JApplicationHelper', '\\Joomla\\CMS\\Application\\ApplicationHelper', '5.0'); // ~/libraries/src/Application/ApplicationHelper.php
                    - ...

                // Ensure FOF autoloader included - needed for things like content versioning where we need to get an FOFTable Instance
                if (!class_exists('FOFAutoloaderFof'))
                {
                    include_once JPATH_LIBRARIES . '/fof/include.php';
                }

                // Register a handler for uncaught exceptions that shows a pretty error page when possible
                set_exception_handler(array('JErrorPage', 'render'));

                // Set up the message queue logger for web requests
                if (array_key_exists('REQUEST_METHOD', $_SERVER))
                {
                    JLog::addLogger(array('logger' => 'messagequeue'), JLog::ALL, array('jerror'));
                }

                // Register JArrayHelper due to JRegistry moved to composer\'s vendor folder
                JLoader::register('JArrayHelper', JPATH_PLATFORM . '/joomla/utilities/arrayhelper.php');

                // Register the Crypto lib
                JLoader::register('Crypto', JPATH_PLATFORM . '/php-encryption/Crypto.php');

                // Register classes where the names have been changed to fit the autoloader rules
                // @deprecated  4.0
                JLoader::register('JInstallerComponent',  JPATH_PLATFORM . '/cms/installer/adapter/component.php');
                JLoader::register('JInstallerFile',  JPATH_PLATFORM . '/cms/installer/adapter/file.php');
                JLoader::register('JInstallerLanguage',  JPATH_PLATFORM . '/cms/installer/adapter/language.php');
                JLoader::register('JInstallerLibrary',  JPATH_PLATFORM . '/cms/installer/adapter/library.php');
                JLoader::register('JInstallerModule',  JPATH_PLATFORM . '/cms/installer/adapter/module.php');
                JLoader::register('JInstallerPackage',  JPATH_PLATFORM . '/cms/installer/adapter/package.php');
                JLoader::register('JInstallerPlugin',  JPATH_PLATFORM . '/cms/installer/adapter/plugin.php');
                JLoader::register('JInstallerTemplate',  JPATH_PLATFORM . '/cms/installer/adapter/template.php');
                JLoader::register('JExtension',  JPATH_PLATFORM . '/cms/installer/extension.php');
                JLoader::registerAlias('JAdministrator',  'JApplicationAdministrator');
                JLoader::registerAlias('JSite',  'JApplicationSite');

                // Can be removed when the move of all core fields to namespace is finished
                \Joomla\CMS\Form\FormHelper::addFieldPath(JPATH_LIBRARIES . '/joomla/form/fields');
                \Joomla\CMS\Form\FormHelper::addRulePath(JPATH_LIBRARIES . '/joomla/form/rule');
                \Joomla\CMS\Form\FormHelper::addRulePath(JPATH_LIBRARIES . '/joomla/form/rules');
                \Joomla\CMS\Form\FormHelper::addFormPath(JPATH_LIBRARIES . '/joomla/form/forms');
                \Joomla\CMS\Form\FormHelper::addFieldPath(JPATH_LIBRARIES . '/cms/form/field');
                \Joomla\CMS\Form\FormHelper::addRulePath(JPATH_LIBRARIES . '/cms/form/rule');
```

2. Administrator Site:


## Alias loader
```php
abstract class Loader
{

    public static function registerAlias($alias, $original, $version = false)
    {
        ...
        // Nếu alias chưa được đăng ký (mảng self::$classAliases với key là $alias chưa tồn tại)
        // => đăng ký: self::$classAliases[$alias] = $original; and return true;
        // => đồng thời cũng đăng ký ngược: self::$classAliases[$original] = $alias; 
        return true/false;
    }
}

```