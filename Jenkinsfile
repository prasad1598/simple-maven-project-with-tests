    def pipeline
    node('slave') {
        pipeline = load 'pipeline.groovy'
        pipeline.functionA()
    }
    pipeline.functionB()
