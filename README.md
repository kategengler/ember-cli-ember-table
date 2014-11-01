**NOTE**: This is still a work in progress.

# ember-cli-ember-table

## Installation

* `git clone` this repository
* `cd ember-cli-ember-table`
* `npm install`
* `bower install`

## Test in dummy app locally

* `ember server`
* Visit http://localhost:4200

## Usage (in consuming project)

* `npm install --save [path-to-repo]/ember-cli-ember-table`
* `ember g ember-cli-ember-table`

At this point you can use the component in the templates of your consuming app.

    {{ember-table
      height=400
      hasFooter=false
      enableContentSelection=true
      columnsBinding="columns"
      contentBinding="content"
    }}

You will also need to setup your controller to provide content for the ember-table.

Example controller

    import ColumnDefinition from '../column-definition';

    export default Ember.Controller.extend({
      numRows: 10000,

      columns: function() {
        var dateColumn, openColumn, highColumn, lowColumn, closeColumn;
        dateColumn = Ember.Table.ColumnDefinition.create({
          columnWidth: 150,
          textAlign: 'text-align-left',
          headerCellName: 'Date',
          getCellContent: function(row) {
            return row.get('date').toDateString();
          }
        });
        openColumn = Ember.Table.ColumnDefinition.create({
          columnWidth: 100,
          headerCellName: 'Open',
          getCellContent: function(row) {
            return row.get('open').toFixed(2);
          }
        });
        highColumn = Ember.Table.ColumnDefinition.create({
          columnWidth: 100,
          headerCellName: 'High',
          getCellContent: function(row) {
            return row.get('high').toFixed(2);
          }
        });
        lowColumn = Ember.Table.ColumnDefinition.create({
          columnWidth: 100,
          headerCellName: 'Low',
          getCellContent: function(row) {
            return row.get('low').toFixed(2);
          }
        });
        closeColumn = Ember.Table.ColumnDefinition.create({
          columnWidth: 100,
          headerCellName: 'Close',
          getCellContent: function(row) {
            return row.get('close').toFixed(2);
          }
        });
        return [dateColumn, openColumn, highColumn, lowColumn, closeColumn];
      }.property(),

      content: function() {
        var generatedContent = [];
        for (var i = 0; i < this.get('numRows'); i++) {
          var date = new Date();
          date.setDate(date.getDate() + i);
          generatedContent.push(Ember.Object.create({
            date: date,
            open:  Math.random() * 100,
            high:  Math.random() * 100 + 50,
            low:   Math.random() * 100 - 50,
            close: Math.random() * 100
          }));
        }
        return generatedContent;
      }.property('numRows'),
    ...


For more information on how to setup `ember-table`, please visit [http://addepar.github.io/ember-table] (http://addepar.github.io/ember-table).

For more information on using `ember-cli`, please visit [http://www.ember-cli.com/](http://www.ember-cli.com/).
