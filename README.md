# Settings
Задачи и решения:

1. Добавить в Настройки -- Экран -- тайм-аут экрана в 24 часа (ну или чтобы экран не выключался вообще)

Добавить эти пункты можно через Settings\res\values\arrays.xml 

    <!-- Display settings.  The delay in inactivity before the screen is turned off. These are shown in a list dialog. -->
    <string-array name="screen_timeout_entries">
        <item>15 seconds</item>
        <item>30 seconds</item>
        <item>1 minute</item>
        <item>2 minutes</item>
        <item>5 minutes</item>
        <item>10 minutes</item>
        <item>30 minutes</item>
        <!-- ScrubberMods -->
        <item>24 hours</item>
        <item>Never</item>
    </string-array>

    <!-- Do not translate. -->
    <string-array name="screen_timeout_values" translatable="false">
        <!-- Do not translate. -->
        <item>15000</item>
        <!-- Do not translate. -->
        <item>30000</item>
        <!-- Do not translate. -->
        <item>60000</item>
        <!-- Do not translate. -->
        <item>120000</item>
        <!-- Do not translate. -->
        <item>300000</item>
        <!-- Do not translate. -->
        <item>600000</item>
        <!-- Do not translate. -->
        <item>1800000</item>
        <!-- ScrubberMods -->
        <item>86 400 000</item>
        <item>0</item>
    </string-array>

Для последующего использования можно сделать vendor/overlay готовую "дополнялку" настроек..

2. Вырезать в Настройках пункт LiveDisplay и Trust

2.1 LiveDisplay:

Отключение функции LiveDisplay через bool в org.lineageos.platform-res

org.lineageos.platform-res\res\values\bools.xml <bool name="config_enableLiveDisplay">true</bool>  заменить на <bool name="config_enableLiveDisplay">false</bool> и удалить org.lineageos.livedisplay.xml в system/etc/permissions/

Изменить значения bool в \org.lineageos.platform-res\res\values\config.xml:   
<bool name="config_enableLiveDisplay">true</bool> true to false

удалить org.lineageos.livedisplay.xml в */permissions/

В Settings\res\xml\display_settings.xml удалить пункт:

    <org.lineageos.internal.lineageparts.LineagePartsPreference
        android:key="livedisplay"
        lineage:requiresConfig="@*lineageos.platform:bool/config_enableLiveDisplay" />

!!!!!!!Или если хотис сделать этот не активным.."не нажимаемым", то достаточно добавить в Preference атрибут android:selectable="false" !!!!!!
	
2.2 Trust 

Для отключения Trust необходимо:

Изменить значения bool в \Settings\res\values\config.xml:   
<bool name="config_show_manage_trust_agents">true</bool> true to false
<bool name="config_show_trust_agent_click_intent">true</bool> true to false

Удалить пункт Preference в \Settings\res\xml\security_dashboard_settings.xml:

    <Preference
        android:order="70"
        android:key="manage_trust_agents"
        android:title="@string/manage_trust_agents"
        android:summary="@string/summary_placeholder"
        android:fragment="com.android.settings.security.trustagent.TrustAgentSettings" />


!!!!!!!Или если хотис сделать этот не активным.."не нажимаемым", то достаточно добавить в Preference атрибут android:selectable="false" !!!!!!
