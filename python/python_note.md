## flask
### Blueprint 蓝图
定义单应用的视图，模板，静态文件等等的集合
app
  web
    view
      webrestful.py
        bp = Blueprint('report', __name__, url_prefix='/test', template_folder='templates', static_folder='static')
        @bp.route("/hello", methods=["GET"])
        def hello():
          param = resquest.arg.get('param')
          return jsonify(msg='hello_get')
        @bp.route("/hello", methods=["POST"])
        def hellopost():
          data = resquest.get_json()
          return jsonify(msg='hello_post')
