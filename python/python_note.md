## flask
### Blueprint 蓝图
定义单应用的视图，模板，静态文件等等的集合
app
  web
    view
      webrestful.py
        bp = Blueprint('report', __name__, url_prefix='/web/task', template_folder='templates', static_folder='static')
