# Создать портфель

Чтобы создать портфель проектов:

1. Перейдите на любую страницу, с которой можно создать портфель:

   * На панели слева выберите ![](../../_assets/tracker/svg/project.svg)&nbsp;**{{ ui-key.startrek.blocks-desktop_b-queues-info.projects }}**, затем нажмите **Создать** → **Портфель**.
   * В [списке портфелей и проектов](my-projects.md) на вкладке **Структура** под списком нажмите **Создать портфель**.
   * В [списке портфелей и проектов](my-projects.md) на вкладке **Список** под списком нажмите **Создать портфель**.

1. Введите название портфеля, установите дату завершения и нажмите **Создать**.

1. На вкладке **{{ ui-key.startrek.ui_components_portfolios_Header.description-tab }}** добавьте информацию:

   * Описание портфеля: над чем вы работаете и каких целей хотите достичь.
   * Прикрепленные файлы: рабочие материалы портфеля.
   * Чеклист: список значимых этапов или целей портфеля.
   * **{{ ui-key.startrek.ui_components_Project.sidebar-param-title--status }}**: укажите, на каком этапе находится портфель.
   * **{{ ui-key.startrek.ui_components_Project.sidebar-param-title--startDate }}** и **{{ ui-key.startrek.ui_components_Project.sidebar-param-title--endDate }}**.
   * **{{ ui-key.startrek.ui_components_Project.sidebar-param-title--lead }}**, **{{ ui-key.startrek.ui_components_Project.sidebar-param-title--clients }}** и **{{ ui-key.startrek.ui_components_Project.sidebar-param-title--teamUsers }}**: начните вводить имя или логин сотрудника и выберите подходящий вариант из списка.
   * **{{ ui-key.startrek.ui_components_Project.sidebar-param-title--tags }}**: добавьте или выберите теги, с помощью которых будет проще найти нужный портфель.

## Связать портфели и проекты {#add-portfolios-projects}

#### Добавить вложенный портфель или проект {#add-nested}

1. Откройте окно создания одним из способов:
   * На странице портфеля в правом верхнем углу нажмите **Добавить** и выберите **Портфель** или **Проект**.
   * На странице портфеля перейдите на вкладку **Проекты** и нажмите **Добавить проект** или **Добавить портфель**.
1. Заполните окно создания проекта или портфеля:
   * Чтобы создать новый проект или портфель: 
      1. Выберите **Новый**.
      1. Укажите название проекта или портфеля, при желании  или сбросьте дату завершения и нажмите **Создать**.

         {% note alert %}
         
         В качестве даты завершения по умолчанию выставляется конец текущего квартала.

         {% endnote %}

   * Чтобы добавить существующий проект или портфель:
      1. Выберите **Существующий**.
      1. Начните вводить название проекта или портфеля и выберите подходящий вариант из списка.

#### Добавить родительский портфель

1. Перейдите на страницу проекта или портфеля и на панели справа нажмите **Входит в портфель**.
1. Начните вводить название портфеля и выберите подходящий вариант из списка.
1. Нажмите **Сохранить**.

## Удалить портфель {#delete}

{% note alert %}

Удалить портфель может его автор и пользователь, указанный в поле **{{ ui-key.startrek.ui_components_Project.sidebar-param-title--lead }}**.

{% endnote %}

Чтобы удалить портфель:

1. На панели слева выберите ![](../../_assets/tracker/svg/project.svg)&nbsp;**{{ ui-key.startrek.blocks-desktop_b-queues-info.projects }}** или перейдите по [прямой ссылке]({{ link-tracker }}pages/projects) и откройте страницу портфеля.

1. В правом верхнем углу страницы нажмите ![](../../_assets/horizontal-ellipsis.svg) и выберите **{{ ui-key.startrek.ui_components_portfolios_PortfolioMenu.remove-portfolio }}**.