Ant
===========================

.. sourcecode:: groovy

  task hello1 << {
    ant.echo(message: 'hello1')
  }

  task hello2 << {
    ant {
      echo(message: 'hello1')
    }
  }