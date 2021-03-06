# Yii2 jQuery TagEditor widget

Widget for tags adding. Based on https://goodies.pixabay.com/jquery/tag-editor/demo.html

Installation
The preferred way to install this extension is through composer.

```
composer require --prefer-dist soless/yii2-jquery-tageditor-widget "*"
```

usage:
```php
  <?php echo $form->field($model, 'selectedTags')->widget('soless\tageditor\TagEditorWidget', [
	'availableTags' => ['firstTag', 'secondTag', 'thirdTag', ],
        'tagEditorOptions' => [
            'forceLowercase' => false,
            'autocomplete' => [
                'source' => \yii\helpers\Url::toRoute(['/tag/suggest'])
            ],
        ]
    ]) ?>
 ```
 

 app\controllers\TagController (suggest action example) :
  ```php
     public function actionSuggest($term) {
	Yii::$app->response->format = \yii\web\Response::FORMAT_JSON;

        return \yii\helpers\ArrayHelper::getColumn(
	    \common\models\Tag::find()
	    ->select('title')
	    ->filterWhere(['like', 'title', $term.'%', false])
	    ->all(), 
	    'title'
	);
    }
 ```
